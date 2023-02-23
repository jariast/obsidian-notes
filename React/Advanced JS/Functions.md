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

