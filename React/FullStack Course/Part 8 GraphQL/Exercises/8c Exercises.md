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


