# Type Guards

TypeScript follows possible paths of execution that our programs can take to analyze the most specific possible type of a value at a given position.

```ts
typeof padding === "number"
```

# Discriminated Unions

[Docs Link](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#discriminated-unions)

When every type in a union contains a common property with literal types, TypeScript considers that to be a _discriminated union_, and can narrow out the members of the union.

```ts
interface Circle {
  kind: "circle";
  radius: number;
}
 
interface Square {
  kind: "square";
  sideLength: number;
}
 
type Shape = Circle | Square;
```

In the above example, the `kind` property is a *discriminant* property, because if we type check against that property, we can get rid of all other types that don't have that property with the checked value.

```ts
function getArea(shape: Shape) {
  if (shape.kind === "circle") {
    return Math.PI * shape.radius ** 2;
}
```

Above, when we check for the `kind` circle, we're excluding all the other types (Square).

# Functions
## Generic Functions

[Docs](https://www.typescriptlang.org/docs/handbook/2/functions.html#generic-functions)

Generics are used when we want to describe a correspondence between two values.
```ts
function firstElement<Type>(arr: Type[]): Type | undefined {
  return arr[0];
}
```
By adding the `Type` parameter and using it in two places, we've created a link between the input and the output.

### Constraints


