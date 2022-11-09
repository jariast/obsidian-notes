#redux #best-practices
# When to use Redux store
- Do other components need this data?
- Do you need to create more date based in this data?
- Is the same data used to drive sevearl components?
- Do you need to cache the data?
- Do you want to keep the data consisten while hot-reloading UI components?

# Example App Repo

[Github Link](https://github.com/reduxjs/redux-essentials-example-app)

#redux-setup
# How is the initial setup of Redux?
- Install react-redux, redux and @reduxjs/toolkit
- We need to create a slice:
	
```js
import { createSlice } from '@reduxjs/toolkit'

const initialState = [
  { id: '1', title: 'First Post!', content: 'Hello!' },
  { id: '2', title: 'Second Post', content: 'More text' }
]

const postsSlice = createSlice({
  name: 'posts',
  initialState,
  reducers: {}
})

export default postsSlice.reducer

```

- Import that slice into app/store.js
```js
import { configureStore } from '@reduxjs/toolkit'

import postsReducer from '../features/posts/postsSlice'

export default configureStore({
  reducer: {
    posts: postsReducer
  }
})
```

- In index.js we must provide the store
```js
import store from './app/store'
import { Provider } from 'react-redux'
import * as serviceWorker from './serviceWorker'

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
)
```

# Immer Basics
#immer
## Mutate or Return a state object
#stateMutation 
It's extremely important to remember to mutate an object or return a new one, *never* do both. [Here](https://immerjs.github.io/immer/return/) are some examples of correct and incorrect state mutations.