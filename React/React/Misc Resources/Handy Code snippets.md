# Local Storage Custom Hook

In the Custom Hooks workshop, we use a really neat hook: [[Custom Hooks#Custom Local Storage hook]]

# Promise deferring

In the Testing Workshop, in the Mocking Browser APIs section there's a function to manage promises:

```js
function deferred() {
  let resolve, reject;
  const promise = new Promise((res, rej) => {
    resolve = res;
    reject = rej;
  });
  return { promise, resolve, reject };
}
```

