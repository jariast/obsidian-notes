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