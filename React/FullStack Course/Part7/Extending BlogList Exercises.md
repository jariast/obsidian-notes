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