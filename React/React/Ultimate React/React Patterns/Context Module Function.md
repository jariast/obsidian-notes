This pattern encapsulates a complex set of state changes into a utility function.

Example:

```js
function handleSubmit(event) {
    event.preventDefault()
    userDispatch({type: 'start update', updates: formState})
    userClient.updateUser(user, formState).then(
      updatedUser => userDispatch({type: 'finish update', updatedUser}),
      error => userDispatch({type: 'fail update', error}),
    )
  }
```
Above we have a function inside the component that consumes a custom Hook that returns the *state* and the *dispatch* function. `handleSubmit` is in charge of all the update logic, when we apply the pattern, the *consuming component* should only be worried about calling a single function:

```js
const updateUser = (dispatch, user, updates) => {
  dispatch({type: 'start update', updates})
  userClient.updateUser(user, updates).then(
    updatedUser => dispatch({type: 'finish update', updatedUser}),
    error => dispatch({type: 'fail update', error}),
  )
}
```

```js
function handleSubmit(event) {
    event.preventDefault()
    updateUser(userDispatch, user, formState)
}
```

After watching the Solution video, I think it's a good idea to have the function like this:

```js
async function updateUser(dispatch, user, updates) {
  dispatch({type: 'start update', updates})
  try {
    const updatedUser = await userClient.updateUser(user, updates)
    dispatch({type: 'finish update', updatedUser})
    return updatedUser
  } catch (error) {
    dispatch({type: 'fail update', error})
    return Promise.reject(error)
  }
}
```

That way the *consumer* can access the `updatedUser` or the *error* if they need to do something with that.