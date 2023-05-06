[Docs](https://redux.js.org/tutorials/essentials/part-1-overview-concepts#terminology)
# Actions

An action is a JS object that has a `type` field. It can be thought as an event that describes something that happened in the app.

## Action Creators

They are functions that return an action object, they are used to avoid manually creating an action object every time.

# Reducers

A Redux reducer is similar to a JS array reducer. They receive the current *state* and an *action* object, decide how to update the state and return a *new* state.

## Reducers rules:

- They should only use the `state` and `action` arguments to calculate the new state.
- They can only make immutable updates.
- Can't do any async logic, calculate random values or cause any side effects.

# Store

Stores are *objects* where the Redux app state lives.

## Dispatch

The only way to update the state stored in the store is to call the method `store.dispatch` with an action object as argument.

The store will run the reducer function and save the new state.

## Selectors
Selectors are functions the know how to extract specific pieces of data.
