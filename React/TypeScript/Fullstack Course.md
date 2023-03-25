# Utility Types

[Docs](https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys)

We can use utility types to construct  *special* versions of a Type we previously defined, for example, we can remove sensitive information before returning it to a client app. 

# Type guards

[Docs](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#typeof-type-guards)

When we do checks like `typeof argument === 'number'`, TS analyzes the execution path of the code and narrows the Type of it according to it. 

## Type predicates

We can build our own type guards by creating a function which return type is a `type predicate`. The predicate takes the form `<paramName> is <Type>` where the `<paramName>` is the name of a parameter in the current function signature. The return value of the function has to be a Boolean.

# Type assertions

[Docs](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-assertions)

Sometimes we (the developer) know what is the type of value, that TS has no way of knowing, for example when parsing a value or when dealing with external data. We can use the `as` operator to coerce a value into certain type:

```ts
const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;
```

Here the dev knows that when we pass the id `main_canvas` we'll always get an `HTMLCanvasElement`.

