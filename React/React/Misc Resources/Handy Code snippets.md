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

We can use like this:

```js
const { promise, resolve } = deferred();
...
window.navigator.geolocation.getCurrentPosition.mockImplementation(
	(callback) => {
	  promise.then(() => callback(fakePosition));
	}
);

....

resolve();
await promise;
```

# Testing Utils

In Testing Workshop, in the 8th section (Context and Custom Render method) the 3rd Extra Credit talks about replacing the default `render` method of RTL for a custom one which have all the required Context Providers.

I think that the [video](https://epicreact.dev/modules/testing-react-apps/context-and-custom-render-method-extra-credit-solution-3) explains really well the process. Here's the example util:

```js
import * as React from 'react'
import {render as rtlRender} from '@testing-library/react'
import {ThemeProvider} from 'components/theme'

function render(ui, {theme = 'light', ...options} = {}) {
  const Wrapper = ({children}) => (
    <ThemeProvider initialTheme={theme}>{children}</ThemeProvider>
  )
  return rtlRender(ui, {wrapper: Wrapper, ...options})
}

export * from '@testing-library/react'
// override React Testing Library's render with our own
export {render}

```

In the above example the app only requires the `ThemeProvider` but we can provide Router, etc etc