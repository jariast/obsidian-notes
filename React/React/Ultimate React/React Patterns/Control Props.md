## Exercise Extra 01

On this [Extra Credit](https://epicreact.dev/modules/advanced-react-patterns/control-props-extra-credit-solution-1) we must show a Warning on console when the `useToggle` hook is used in a "controlled" way without passing an `onChange` function o a `readOnly` property. The final solution uses [[Hooks#[useEffect](https://beta.reactjs.org/reference/react/useEffect) |useEffect]] to show the warning ONLY in the Initial render (it has several dependencies, but they will never change though):

```js
 React.useEffect(() => {
    warning(!(!hasOnChange && onIscontrolled && !readOnly), 'Error')
  }, [hasOnChange, onIscontrolled, readOnly])
```

We also used the `warning` package that it seems useful for this kind of use cases. 