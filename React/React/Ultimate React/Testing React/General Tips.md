- Don't test implementation details.
- Make sure to use the correct [queries](https://testing-library.com/docs/queries/about/#priority).
- Use a library like [user-event](https://github.com/testing-library/user-event/tree/1af67066f57377c5ab758a1215711dddabad2d83) to simulate user interactions.
	For example, avoid manually clicking an element:
```js
	fireEvent.click(increment)
```

When a real user clicks an element, is firing several events like hover, focus, etc. So instead we could use the `fireEvent` function:

```js
await userEvent.click(increment)
```
- We can use `screen.debug()` so we can see the entire structure of the HTML in the testing console.
- Use [faker](https://www.npmjs.com/package/@faker-js/faker) to generate fake data.
- Use [jest-dom](https://github.com/testing-library/jest-dom) assertions.
- Solving act warnings [blog post](https://kentcdodds.com/blog/fix-the-not-wrapped-in-act-warning).
- Override RTL's default `render` method as explained in [[Handy Code snippets#Testing Utils]]