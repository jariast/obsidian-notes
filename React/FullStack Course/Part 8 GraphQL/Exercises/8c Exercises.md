# Setup
#backendSetup #security #environment

- Install mongoose
``` bash
npm install mongoose
```

- Install [dotenv](https://github.com/motdotla/dotenv)
```bash
npm install dotenv --save
```

- Install [cross-env](https://www.npmjs.com/package/cross-env) for Windows compatibility.

```bash
npm install --save-dev cross-env
```

We add a `.env` file with the DB URI and the App secret. Remember to add the this file to `.gitignore`.

We must call `require('dotenv').config()` in the `app.js` file to ensure that the variables setup in `.env` file are available.

In `package.json` we modified the scripts like this:

```json
"dev": "cross-env NODE_ENV=development nodemon index.js"
```


# 8.13: Database, part01

I was facing a bug when changing the queries from arrays to using the DB, I forgot to use the `async` keyword in the start of the function.

It was really crucial to understand that the Author was no longer a String and it is indeed another entire schema, so when Adding a New Book, we needed to add the Author's ID to the Book object and not just its name or  any other object.