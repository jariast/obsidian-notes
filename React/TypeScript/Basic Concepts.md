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

## Exhaustiveness checking
[Docs](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#exhaustiveness-checking)

Exhaustiveness checking makes use of the `never` type to ensure that we're handling every case of a Type Union.
```ts
type Shape = Circle | Square;
function getArea(shape: Shape) {
  switch (shape.kind) {
    case 'circle':
      return Math.PI * shape.radius ** 2;
    case 'square':
      return shape.sideLength ** 2;
    default:
      const _exhaustiveCheck: never = shape;
      return _exhaustiveCheck;
  }
}
```

If we add a new type `Triangle` and we forget to add a case for it, TypeScript will throw an error telling us that the type `Triangle` is not assignable to type `never`.

# Functions

## Type Parameters
They are placeholders for a specific data type that can be specified later.

A type parameter is declared like `<T>` before the function or class that uses it.

## Generic Functions

[Docs](https://www.typescriptlang.org/docs/handbook/2/functions.html#generic-functions)

Generics are used when we want to describe a correspondence between two values.
```ts
function firstElement<Type>(arr: Type[]): Type | undefined {
  return arr[0];
}
```
By adding the `Type` parameter and using it in two places, we've created a link between the input and the output.

## Constraints
[Docs](https://www.typescriptlang.org/docs/handbook/2/functions.html#constraints)

```ts
function longest<Type extends { length: number }>(a: Type, b: Type) {
  if (a.length >= b.length) {
    return a;
  } else {
    return b;
  }
}
```

In the above function, we constrained the parameters to have the property `length: number` so we can call `longest` with two `arrays`  or `strings`, the important thing is that they have a `lenght` property.

## Guidelines
[Docs](https://www.typescriptlang.org/docs/handbook/2/functions.html#guidelines-for-writing-good-generic-functions)

- Use fewer type parameters.
- Push Type Parameters "down"