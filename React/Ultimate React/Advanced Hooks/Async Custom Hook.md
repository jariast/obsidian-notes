# Dependencies issues.

I had this code:

```js
React.useEffect(() => {
	const promise = asyncCallback()
	if (!promise) {
	  return
	}
	
	dispatch({type: 'pending'})
	promise.then(
	  data => {
		dispatch({type: 'resolved', data})
		console.log('Dispatching', 'Resolved')
	  },
	  error => {
		dispatch({type: 'rejected', error})
		console.log('Dispatching', 'Error')
	  },
	)
	}, [dependencies[0]])
  ```
It was kind of working but I'm a huge idiot, the dependencies variables was already an array, so the dependencies array just needs that variable, it doesn't need to be "wrapped" inside another array.

```js
React.useEffect(() => {
    ///.... omitting rest of code
  }, dependencies)
  ```

# Returning a memoized function 

In the Extra Number 2, we had to return a memoized function that was to be consumed by the consumer of the custom hook. I had almost all the Exercise done, but was thrown off by the dependencies array again, turns out that we just needed to pass an empty array, so the function will be created only in the Initial Render.

```js
const run = React.useCallback(promise => {
    dispatch({type: 'pending'})
    promise.then(
      data => {
        dispatch({type: 'resolved', data})
        console.log('Dispatching', 'Resolved')
      },
      error => {
        dispatch({type: 'rejected', error})
        console.log('Dispatching', 'Error')
      },
    )
  }, [])
  ```
  