# Exercise 01

I was having an issue rendering the root component like this:

```js
const div = document.createElement('div')
document.body.append(div)

const root = createRoot(div)
root.render(<Counter />)
```

The test was generating an error:

`Warning: An update to Root inside a test was not wrapped in act(...).`

To fix it I needed to wrap the `root.render` method in the `act` function:
```js
act(() => {
	root.render(<Counter />)
})
  ```

