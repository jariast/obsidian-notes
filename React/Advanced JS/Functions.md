# First Class Functions
Everything you can do with other types, you can do with functions as well. Assign them to variables, pass them around, create them on the fly. @!!!

# Statements vs Expressions

## Expression
A expression is a unit of code that results in a value.

```js
a = 3 // This results in 3
3 + 2 // This results in 5

let func = () => {} // This is a function expression using arrow syntax

let func = function() { // This is a function expression using anonymous function syntax
}

```

## Statement

```js
if(*expression goes here*)// If is an statement 

function greet() { // This a function statement
	console.log('hi')
}
```

# IIFE

Immediately Invoked Function Expressions

```js
let firstName = 'John';

((name) => {
	console.log(`Hello ${name}`);
})(firstName)
```

IIFE are useful for avoiding polluting the global namespace and for executing `async` functions. The latter use is the most useful nowadays.
```js
const getFileStream = async (url) => {
  // implementation
};

(async () => {
  const stream = await getFileStream("https://domain.name/path/file.ext");
  for await (const chunk of stream) {
    console.log({ chunk });
  }
})();
```

# Bind, call and apply

## Bind

The `bind` method returns a copy of a function with a new `this` value, the new value is the argument provided to the `bind` method.

## Call

The `call` method takes a new `this` value as arguments, it also takes additional arguments for the function separated by commas

```js
let logName = (lang1, lang2) => {
	console.log('Lang1: ', lang1);
	console.log('Lan2: ', lang2);
}

logName.call(
  person, //this is the new *this* value
  'es',
  'en'
);
```

Apply

Similarly to the `call` method, the `apply` method invokes the function with a new `this` value, but it takes instead an array with the function arguments:

```js
logName.call(
  person, //this is the new *this* value
  ["es", "en"]
);
```
