# @types/{npm_package}

TypeScript expects all globally-used code to be typed. The default typings only contains types for TypeScript itself. For example if we're using Node and we want to use the `process.argv` in Node, in older npm versions TypeScript would complain about missing Types definitions.

We can install Types packages by installing community packages. The @types org usually have up to date type defs for most packages.

For most projects in the course we can use something like this:

``` bash
npm install --save-dev @types/react @types/express @types/lodash @types/jest @types/mongoose
```

Notice that we're installing them as Dev dependencies, the type definitions are not needed for a Production build.

# Express Setup

#backendSetup 

Install Express:
```bash
npm i Express
```

Express Types Definitions:
```bash
npm install --save-dev @types/express
```

ts-node-dev is used to recompile the server code during Development:

```bash
npm install --save-dev ts-node-dev
```