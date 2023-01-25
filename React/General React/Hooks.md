# useLayoutEffect
#hook 
This hook is very similar to *useEffect* hook, but it will run as soon as the DOM finishes mutating, **BEFORE** the browser paints the new changes. Very useful to avoid flickering of content. [Useful link with explanation](https://dev.to/emmanuelthecoder/useeffect-vs-uselayouteffect-the-difference-and-when-to-use-them-124c)

# Hooks with dependencies array

When passing a dependencies array to a hook we should consider how it will affect the execution of the hook:

-   Empty Array: The Effect will only run after the initial render.
-   No Dependency Array: The Effect will run every render of the component.
-   Array with dependencies: Effect will run after initial render and after re-renders where the dependencies changed.

# useEffect

The useEffect hook's *setup function* should return a *cleanup function*. 

The execution cycle of *useEffect* is like this:

1. The *setup function* is ran when the component is mounted.
2. When the *dependencies* have changed:
	- The *cleanup function* will run with the old props and state.
	- The *setup function* will run with the new props and state.
3. The *cleanup function* will run one last time when the component unmounts.

[React docs](https://beta.reactjs.org/reference/react/useEffect#connecting-to-an-external-system)

# useReducer

It takes three arguments:

-   A reducer function, that is responsible of updating the State according to the dispatch function.
-   Initial State.
-   An optional Initializer function for Lazy Init.