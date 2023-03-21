# Project Setup
#backendSetup #setup 

We'll install Typescript:

```shell
 npm install typescript --save-dev
```

Add this line to the scripts in `package.json`:
```json
"tsc": "tsc"
```

Initialize TS config:
```shell
 npm run tsc -- --init
```

We should modify the `tsconfig.json` file to contain the following:

```json
{
  "compilerOptions": {
    "target": "ES6",
    "outDir": "./build/",
    "module": "commonjs",
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "esModuleInterop": true
  }
}
```

Install Express, types and ESlint:

```shell
npm install express
npm install --save-dev eslint @types/express @typescript-eslint/eslint-plugin @typescript-eslint/parser
```

Create a `.eslintrc` file with the following content:

```shell
touch .eslintrc
```

```json
{
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:@typescript-eslint/recommended-requiring-type-checking"
  ],
  "plugins": ["@typescript-eslint"],
  "env": {
    "browser": true,
    "es6": true,
    "node": true
  },
  "rules": {
    "@typescript-eslint/semi": ["error"],
    "@typescript-eslint/explicit-function-return-type": "off",
    "@typescript-eslint/explicit-module-boundary-types": "off",
    "@typescript-eslint/restrict-template-expressions": "off",
    "@typescript-eslint/restrict-plus-operands": "off",
    "@typescript-eslint/no-unsafe-member-access": "off",
    "@typescript-eslint/no-unused-vars": [
      "error",
      { "argsIgnorePattern": "^_" }
    ],
    "no-case-declarations": "off"
  },
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "project": "./tsconfig.json"
  }
}
```

Create a `.eslintignore` file and add `build/index.js` to it, this way ESlint won't complain about any issues in there.

Install `ts-node-dev` so we can have a hot reloading server ready:

```shell
npm install --save-dev ts-node-dev
```

Add the following scripts to `package.json`:
```json
{
  // ...
  "scripts": {
    "tsc": "tsc",
    "dev": "ts-node-dev index.ts",
    "lint": "eslint --ext .ts .",
    "start": "node build/index.js" // This to run in prod mode
	},
    // ...
}
```

Install CORS and its types:

```bash
npm install cors
npm install --save @types/cors
```

Import CORS:
```ts
import cors = require('cors');
...
app.use(cors())
```


## Production Build
Let's try to create a _production build_ by running the TypeScript compiler. Since we have defined the `outdir` in our `tsconfig.json`, nothing's left but to run the script `npm run tsc.`

# Project structure
#backendSetup 

- We'll move all of source code into a `src` folder (including `index.ts`).
- The routes go in separate files e.g. `src/routes/patients.ts`.
- The `index.ts` file is in charge of routing all the specific routes to the correct router:

```ts
import patientRouter from './routes/patients'
...
...

app.use('api/patients', patientRouter)
```

- The data manipulations will be handled by a separate file, a service. The services go in the `src/services` folder and can be named like `patientService`.
- We can have all the type definitions inside a `Types` file, where we export all the definitions.
- If we're using some `json` file as the source of data it  is a good idea to convert it to a TypeScript file and export the data using the correct Type definitions that we require. Sometimes if we import the JSON file directly, we would have to make a `Type Assertion` and they should be avoided as much as possible.
- Within a single directory, it is important to name all the valid Modules with different extensions, something unique. Please refer to [the course](https://fullstackopen.com/en/part9/typing_an_express_app#node-and-json-modules) for a detailed explanation.

# Receiving data from external sources (client data)

It is good practice to have a function that checks that all the data we're getting from the client is valid, we can create a util function that receives the raw data and then returns the Object we expect. Something like:

```ts
const toNewPatient = (object: unknown): NewPatientEntry =>{...}
```

There are 2 noteworthy things here:
- The type of the `object` parameter is `unknown`, because we can't exactly know what the external system is sending (in our case the web app), we should use this data type to later construct the required object.
- The `NewPatientEntry` data type is created using the `Omit` [[Fullstack Course#Utility Types | utility]] type, we're going to omit the ID field because we must first generate it.

## Parsing fields
When parsing a string we can use the following function:

```js
const parseComment = (comment: unknown): string => {
  if (!comment || !isString(comment)) {
    throw new Error('Incorrect or missing comment');
  }

  return comment;
};
```

And use this type guard:

```ts
const isString = (text: unknown): text is string => {
  return typeof text === 'string' || text instanceof String;
};
```

Here we're using a custom [[Fullstack Course#Type guards |type guard]], notice the [[Fullstack Course#Type predicates|predicate]] `text is string`, in this case we could've just the regular type guard `instanceof` but we wanted to be extra careful and check for strings created using the `string constructor` and the far most popular string literal.

## Parsing to an Enum field
