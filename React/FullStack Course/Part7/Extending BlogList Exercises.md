# 7.10 Redux, step2

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
