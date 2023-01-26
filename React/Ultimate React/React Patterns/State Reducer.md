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

In the c

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