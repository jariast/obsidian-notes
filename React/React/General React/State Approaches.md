

# Declarative approach to UI building:

[Docs](https://react.dev/learn/reacting-to-input-with-state)
1.  **Identify** your component’s different visual states
2.  **Determine** what triggers those state changes
3.  **Represent** the state in memory using `useState`
4.  **Remove** any non-essential state variables
5.  **Connect** the event handlers to set the state

# Displaying many states:

It can be useful to render the component with each different state it has. [Docs](https://react.dev/learn/reacting-to-input-with-state#displaying-many-visual-states-at-once)

# Structuring state:
[Docs](https://react.dev/learn/choosing-the-state-structure#principles-for-structuring-state)

1.  **Group related state.** If you always update two or more state variables at the same time, consider merging them into a single state variable.
2.  **Avoid contradictions in state.** When the state is structured in a way that several pieces of state may contradict and “disagree” with each other, you leave room for mistakes. Try to avoid this.
3.  **Avoid redundant state.** If you can calculate some information from the component’s props or its existing state variables during rendering, you should not put that information into that component’s state.
4.  **Avoid duplication in state.** When the same data is duplicated between multiple state variables, or within nested objects, it is difficult to keep them in sync. Reduce duplication when you can.
5.  **Avoid deeply nested state.** Deeply hierarchical state is not very convenient to update. When possible, prefer to structure state in a flat way.