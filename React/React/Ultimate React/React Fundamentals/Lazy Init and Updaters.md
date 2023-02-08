[Kent's Blog](https://kentcdodds.com/blog/use-state-lazy-initialization-and-function-updates)

[React Docs about Updaters](https://beta.reactjs.org/learn/queueing-a-series-of-state-updates#updating-the-same-state-variable-multiple-times-before-the-next-render)

# Updaters

When you need to compute a new state using the previous value of the state, you should use state updater. Instead of telling React what the *next value IS* we pass a function that tells React *HOW  to calculate* the new value from the *previous one*.

Example:

```jsx
<button onClick={() => {
	setNumber(n => n + 1);
	setNumber(n => n + 1);
	setNumber(n => n + 1);
  }}>+3</button>
```

![[Pasted image 20230114112811.png]]

When React renders after the user clicks the button, React goes trough the queue of updaters and calls them in order. 

# Lazy State
[React docs (old)](https://reactjs.org/docs/hooks-reference.html#lazy-initial-state)

When we need to run an expensive computation on the *Initial* render of a component we can pass a function to `useState` to tell React to run it only in the Initial render.

```js
const initialState = Number(window.localStorage.getItem('count'))
const [count, setCount] = React.useState(initialState)
```