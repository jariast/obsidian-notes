This pattern enables you to provide a set of components that implicitly share state for a simple yet powerful declarative API for reusable components.

```js
function Toggle({children}) {
  const [on, setOn] = React.useState(false)
  const toggle = () => setOn(!on)

  return (
    <ToggleContext.Provider value={{on, toggle}}>
      {children}
    </ToggleContext.Provider>
  )
}
```

This component can be used like this:

```jsx
function App() {
  return (
    <div>
      <Toggle>
        <ToggleOn>The button is on</ToggleOn>
        <ToggleOff>The button is off</ToggleOff>
        <div>
          <ToggleButton />
        </div>
      </Toggle>
    </div>
  )
}
```

Each children can access the overall state of the component by reading the `ToggleContext` [[Hooks#useContext | useContext]]. For that we can use a custom hook `useToggle`:

```js
const useToggle = () => {
  const context = React.useContext(ToggleContext)
  console.log('Context: ', context)
  if (typeof context === 'undefined') {
    throw new Error('useToggle must be used within a Toggle')
  }

  return context
}
```
