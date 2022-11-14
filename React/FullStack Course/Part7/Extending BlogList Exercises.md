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

TODO: Actually use `createEntityAdapter` to manage normalized state.

### createEntityAdapter

`createEntityAdapter` API provides a way to store a collection of items in the normalized shape of `{ids: [], entities: {}}`. It will also provide a set of reducer functions and selectors to manage this kind of data arrangement.