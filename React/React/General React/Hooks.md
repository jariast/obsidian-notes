
# Hooks with dependencies array

When passing a dependencies array to a hook we should consider how it will affect the execution of the hook:

-   Empty Array: The Effect will only run after the initial render.
-   No Dependency Array: The Effect will run every render of the component.
-   Array with dependencies: Effect will run after initial render and after re-renders where the dependencies changed.

# [useLayoutEffect](https://beta.reactjs.org/reference/react/useLayoutEffect)
#hook 
This hook is very similar to *useEffect* hook, but it will run as soon as the DOM finishes mutating, **BEFORE** the browser paints the new changes. Very useful to avoid flickering of content. [Useful link with explanation](https://dev.to/emmanuelthecoder/useeffect-vs-uselayouteffect-the-difference-and-when-to-use-them-124c)

# [useEffect](https://beta.reactjs.org/reference/react/useEffect)

The useEffect hook's *setup function* should return a *cleanup function*. 

The execution cycle of *useEffect* is like this:

1. The *setup function* is ran when the component is mounted.
2. When the *dependencies* have changed:
	- The *cleanup function* will run with the old props and state.
	- The *setup function* will run with the new props and state.
3. The *cleanup function* will run one last time when the component unmounts.

[React docs](https://beta.reactjs.org/reference/react/useEffect#connecting-to-an-external-system)

# [useReducer](https://beta.reactjs.org/reference/react/useReducer)

It takes three arguments:

-   A reducer function, that is responsible of updating the State according to the dispatch function.
-   Initial State.
-   An optional Initializer function for Lazy Init.

It returns:

- A stateful value
- A dispatch function, user to update the state via the Reducer function.

# [useCallback](https://beta.reactjs.org/reference/react/useCallback)

It caches a function definition between re-renders. It also has a dependencies array like *useEffect*.

# useContext
[React Docs](https://beta.reactjs.org/reference/react/useContext) 

It's used to read and subscribe to Context from a component.

# [useImperativeHandle](https://beta.reactjs.org/reference/react/useImperativeHandle) 

It's used in conjunction with _forwardRef_ to override the _ref_ exposed to a component's parent, it can be used to expose methods.

# [useRef](https://beta.reactjs.org/reference/react/useRef)

Is used to create a reference value. The value of the reference won't change between re-renders and when you modify it by using `ref.current` it doesn't trigger a re-render.