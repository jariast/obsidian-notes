- Redux actions and state should only contain plain JS values like object, arrays and primitives. Storing class instances or functions is not allowed. For example Date objects must transformed into strings before saving them to the store: #redux #reducers [Adding Dates to posts](https://redux.js.org/tutorials/essentials/part-4-using-data#storing-dates-for-posts)

```js
new Date().toISOString()
```

- If an action needs to contain a unique ID or some other Random value, always generate the value first and put it in the *action payload*. We can do this using the `prepare`  field of the `reducers` field inside the `createSlice` function: #reducers #actions
 ```js
 const postsSlice = createSlice({
  name: 'posts',
  initialState,
  reducers: {
    postAdded: {
      reducer(state, action) {
        state.push(action.payload)
      },
      prepare(title, content) {
        return {
          payload: {
            id: nanoid(),
            title,
            content
          }
        }
      }
    }
    // other reducers here
  }
})
```

- In order to isolate components from state implementation, we could use reusable selector functions inside the slice files: #selectors #sliceFiles
```js
export const selectAllPosts = state => state.posts

export const selectPostById = (state, postId) =>
  state.posts.find(post => post.id === postId)
```
They can be used like this in the component:
```js
// omit imports
import { selectPostById } from './postsSlice'

export const SinglePostPage = ({ match }) => {
  const { postId } = match.params

  const post = useSelector(state => selectPostById(state, postId))
  // omit component logic
}
```

- In one of the [examples](https://redux.js.org/tutorials/essentials/part-6-performance-normalization#showing-new-notifications), we're rendering a list of notifications, in order to avoid 