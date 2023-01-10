# Vite

Is a Webpack and Create React App replacement, I didn't find too much issues while using it. It is FAST, it reloads the app significantly faster.

The only issue that I encountered was when I was trying to use [Styled Components Babel Plugin](https://styled-components.com/docs/tooling#babel-plugin). Honestly, I didn't spent too much time trying to make it work. Apparently what must be done is to install Babel and set it up.

# Resolving import paths

This one was interesting, because I learned how to configure the project to use import paths like:

```js
import Label from '@/atoms/Label';
```

In the case of Vite, I had to add a `jsconfig.json` file:

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "target": "es6",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

And define `vite.config.js` like this:

```js
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import path from 'path';

// https://vitejs.dev/config/
export default defineConfig({
  resolve: {
    alias: [
      { find: '@', replacement: path.resolve(__dirname, './src') },
      { find: '@pages', replacement: path.resolve(__dirname, './src/pages') },
    ],
  },
  plugins: [react()],
});
```

# CDN

I used [Cloudinary](https://cloudinary.com/) for the images in the blog, I found it really easy to use, it seems like images load a little bit slow sometimes, but nothing too bad for a non-prod app.

# ChatGTP

Was a huge help during the entire process, it is really an awesome assistant. I must be careful though, sometimes it responds with slightly wrong information, sometimes it uses and old version of a library, making things not work at all or cause subtle bugs.