[Link](https://fullstackopen.com/en/part7/exercises_extending_the_bloglist)

# 7.11 Redux, step2

## Creating Blog Redux

#solutions #thunk #errorHandling #redux
When using createAsyncThunk, by default when a request fails, it will try to access the `error` property of the server response, as we're using a custom backend, that returns custom errors messages we must use the API utility `rejectWithValue` as shown in the [Redux docs](https://redux-toolkit.js.org/api/createAsyncThunk#handling-thunk-errors) . 
```js
export const createBlog = createAsyncThunk(
  'blogs/createBlog',
  async (newBlog, { rejectWithValue }) => {
    try {
      const response = await blogsService.createBlog(newBlog);
      return response;
    } catch (error) {
      return rejectWithValue(error.response.data.error);
    }
  }
);
```

## Moving Blog Creation logic

I moved the handling of Blog Creation to `BlogsForm.js` file. The obvious advantage of this is that `BlogsList` has a lot less logic in it, one downside that I should review later is how to Toggle the visibility from the `Blogsform` itself. We could use one of the actions in order to update the `status` of the state to have an specific value when a blog is created. #TODO #reviewLater

# 7.12 Redux, step3

## Liking blog
#immer #stateMutation
Is not updating the blog in the state.
Update: I was reassigning the blog, and this is a [Pitfall](https://immerjs.github.io/immer/pitfalls/#dont-reassign-the-recipe-argument) of using Immer. After updating the likes directly on the "old" blog, the state is updating correctly. [[General Info#Immer Basics#Mutate or Return a state object]]

```js
addCase(likeBlog.fulfilled, (state, action) => {
	const updatedBlog = action.payload;
	let existingBlog = state.blogs.find((blog) => {
	  return blog.id === updatedBlog.id;
	});
	if (existingBlog) {
	  existingBlog.likes = updatedBlog.likes;
	}
});
```

This also could be avoided by copying the state and returning a new updated state (the functional programming way).

# 7.13 Redux, step 4

## Users view

We're using a very simple routing implementation: 
```jsx
<Router>
  <h2>blogs</h2>
  <p>{`${user.name} is logged in`}</p>
  <button id="logout-button" onClick={handleLogout}>
	Log out
  </button>
  <Routes>
	<Route path="/users" element={<UsersList />} />
	<Route path="/" element={<BlogsList />} />
  </Routes>
</Router>
```

By default the app we'll load the `BlogsList` component, but if the URL has `users` on its path, it will render the `UsersList`, right now the only way of accessing the Users List is by manually changing the URL.

### Normalizing data

#backend
At this point I think it is important to normalize the state of the app. We are going to follow [Redux guide](https://redux.js.org/tutorials/essentials/part-6-performance-normalization#normalizing-data).
But first, we must make sure that the Backend does not populate the users when querying for blogs. We make the following changes to the backend app:

```js
blogsRouter.get('/', async (request, response) => {
  const shouldPopulate = request.query.populate;
  const blogs = shouldPopulate
    ? await Blog.find({}).populate('user', { username: 1, name: 1 })
    : await Blog.find({});
  response.json(blogs);
});
```

We're defaulting to not populating the user field if the `populate` query parameter is not present or is falsy. We're going to use the same approach with the `users` route, by default we're only going to return the Ids of blogs of an specific user.

### createEntityAdapter

#normalizedData #reducers
`createEntityAdapter` API provides a way to store a collection of items in the normalized shape of `{ids: [], entities: {}}`. It will also provide a set of reducer functions and selectors to manage this kind of data arrangement.

Thins to note on `blogsSlice` file:

- The sortComparer we're using when creating the Adapter, will sort the **IDS** of the blogs, not the blogs themselves, so we must use the `selecBlogsIds` selectors to access the ordered blogs.
- For the blog deletion we're using the `blogAdapter.removeOne` function as a reducer directly.
- We changed the way we rendered the `BlogsList` and `Blog` components. On the List we're using the blogsIds to map each Blog component, we're also waiting for the request to succeed and that the BlogIds array is populated before rendering each `Blog` component.

# 7.15 Individual user view

## Routing woes

In the [Fullstack app](https://fullstackopen.com/en/part7/react_router#parameterized-route-revisited) we're using a very different approach, instead of every Note component being in charge of selecting its state, the App component is using the `useMatch` function to retrieve the Note Id and then passes the `note` to the `Note` element.

In the [Redux tutorial](https://redux.js.org/tutorials/essentials/part-4-using-data#adding-the-single-post-route) they're using a no longer supported way of using Routing:

```jsx
<Route exact path="/posts/:postId" component={SinglePostPage} />
```
This way was removed on V6 of React Router, now we must use the following pattern:

```jsx
<Route path="/users/:userId" element={<User />} />
```

In order to access the Route Params in the `User` component we now must use the `useParams` hook like shown in this [SO thread](https://stackoverflow.com/questions/64782949/how-to-pass-params-into-link-using-react-router-v6).

We'll default to showing a message like "No user found" when reloading the app inside a User route. There are more advanced [implementations](https://reactrouter.com/en/main/start/tutorial#loading-data) where we could load the required data before hand.

We can also tell the app to load the Users and the Blog everytime it loads, this will result in the "No users found" flashin for a second before the User data is available.

## Selecting User's posts

We'll follow [this guide](https://redux.js.org/tutorials/essentials/part-6-performance-normalization#memoizing-selector-functions) on implementing Memoized selectors. Implementation:

```js
export const selectBlogsByUser = createSelector(
  [selectAllBlogs, (state, userId) => userId],
  (blogs, userId) => blogs.filter((blog) => blog.user === userId)
);
```

The createSelector function takes and array of Selector functions as *Inputs* and an OutPut Selector function is in charge of selecting the actual ouput.

# 7.16 Blog View

## Liking Blog revisited

We were updating the state after a Blog Like like this:

```js
const existingBlog = state.entities[updatedBlog.id];
if (existingBlog) {
  existingBlog.likes = updatedBlog.likes;
}
```

But the array with the Blogs Ids was not re-sorting the blogs, this was caused because the Sorting is only triggered by using one of the [CRUD](https://redux-toolkit.js.org/api/createEntityAdapter#crud-functions) functions exposed by the Entity Adapter. 

The new implementation looks like this:

```js
blogsAdapter.updateOne(state, {
  id: updatedBlog.id,
  changes: { likes: updatedBlog.likes++ },
});
```

**NB:** We introduced a bug by updating the likes once again in the changes object. Let's review the entire *Like* flow:

1. User clicks Like
2. The `likeBlog` asyncThunk receives the whole blog, and increments the the blog's likes.
3. The service sends the request to the backend.
4. The backend responds with the entire blog and the `likes` property with the value we set in step number 2.
5. The reducer for the `likeblog.fulfilled` then updates the Blogs state, we were adding another `like` to that blog's likes.

## Single Blog issues

I think the biggest issue we're facing right now is managing what happens when the data required to show a Blog is missing. I think all this can be solved by using Router Loaders but this is something that will have to wait for later lessons.

We also had to changed the blog creation End Point so it wouldn't populate the `user` field from the `blog` response object. #backend #normalizedData 

## Misc changes

I basically moved all the functionality from `Blog.js` to `SingleBlog.js`. 


# 7.17 Navigation

Pretty straightforward implementation of the Navbar.


# 7.18 comments, step1

At first I was considering creating a new whole slice for the Comments, but the requirement for the exercise was really simple, we don't need to store any user info or any other data for the comment, only the comment itself. With that in mind I think that the best approach was to just add a `comments` property to the `Blog` model. 

I'm still not sure if the best approach is the one proposed in the notes for the exercise, in there they advice to use a `post` request, but I'm not creating a new `comment` object, I'm updating a `Blog` object.