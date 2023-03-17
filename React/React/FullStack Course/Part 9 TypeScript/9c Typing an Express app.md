# Project Setup
#backendSetup #setup 

We'll install Typescript:

```shell
 npm install typescript --save-dev
```

The `tsconfig.json` file should contain the following:

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
    "dev": "ts-node-dev index.ts",    "lint": "eslint --ext .ts ."  },
    "start": "node build/index.js" // This to run in prod mode
    // ...
}
```

## Production Build
Let's try to create a _production build_ by running the TypeScript compiler. Since we have defined the `outdir` in our `tsconfig.json`, nothing's left but to run the script `npm run tsc.`

