1. Don't test implementation details.
2. Make sure to use the correct [queries](https://testing-library.com/docs/queries/about/#priority).
3. Use a library like [user-event](https://github.com/testing-library/user-event/tree/1af67066f57377c5ab758a1215711dddabad2d83) to simulate user interactions.
	For example, avoid manually clicking an element:
```js
	fireEvent.click(increment)
```

When a real user clicks an element, is firing several events like hover, focus, etc. So instead we could use the `fireEvent` function:

```js
await userEvent.click(increment)
```
