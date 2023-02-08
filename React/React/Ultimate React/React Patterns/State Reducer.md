State Reducer inverts control overt the state management of a hook or component, to the developer using it.

```js
function useToggle({initialOn = false, reducer = toggleReducer} = {}) {
  const {current: initialState} = React.useRef({on: initialOn})

  const [state, dispatch] = React.useReducer(reducer, initialState)
  const {on} = state

  return {
    on,
    reset,
    toggle,
    getTogglerProps,
    getResetterProps,
  }
}
```

In the code above, we have a custom hook `useToggle` that can take a `reducer` parameter, this parameter allows the consumer of the hook to implement an entirely new Reducer function so it can customize the behavior of the hook.

```js
function toggleReducer(state, {type, initialState}) {
  switch (type) {
    case actionTypes.toggle: {
      return {on: !state.on}
    }
    case actionTypes.reset: {
      return initialState
    }
    default: {
      throw new Error(`Unsupported type: ${type}`)
    }
  }
}
```

If we export  `toggleReducer` the consumer can also override only a portion of the actions, like so:

```js
function toggleStateReducer(state, action) {
    if (action.type === actionTypes.toggle && clickedTooMuch) {
      return {on: state.on}
    }
    return toggleReducer(state, action)
}
```

