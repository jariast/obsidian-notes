React keeps track of the Components it renders by default by using the position of the Component in the [UI Tree](https://beta.reactjs.org/learn/preserving-and-resetting-state#the-ui-tree). 

When we try to render a list of the same Component React tries to rely in the position of the Components in the UI tree, but when you start mutating that position, React can get very confused.

The 'key' prop lets React know which component Instance is which, that's why when we want to reset the component we can usually just change the key of it and React will unmount and mount a completely new Instance.