```js
const callAll = (...fns) => (...args) => fns.forEach(fn => fn?.(...args))

function useToggle() {
  const [on, setOn] = React.useState(false)
  const toggle = () => setOn(!on)

  function getTogglerProps({onClick, ...props} = {}) {
    return {
      'aria-pressed': on,
      onClick: callAll(onClick, toggle),
      ...props,
    }
  }

  return {
    on,
    toggle,
    getTogglerProps,
  }
}
```
The `callAll` function is useful for calling several functions in succession .

The `getToggleProps` function lets the Consumer of the `useToggle` hook do the following:

- Set `aria-pressed` attribute and the `onClick` handler by default.
- The consumer of the hook can attach another function to the `onClick` handler without overriding the default behavior.
- The consumer can pass any other props it requires.