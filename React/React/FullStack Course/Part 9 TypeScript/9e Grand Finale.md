
# Types from other types ?

#complexTypes

In one of the examples we have an Entry Type that has a property `diagnosisCodes` which is an array of `Diagnosis` codes. As the `Diagnosis` type already exists:

```ts
export interface Diagnose {
  code: string;
  name: string;
  latin?: string;
}
```

We can use that type definition to refine our Entry type like this:

```ts
interface Entry{
	...
	diagnosisCodes?: Diagnosis['code'][];
}
```

With the above interface we're telling TS that the `diagnosisCodes` property is an array of the type `codes` of the `Diagnosis` interface. The double array syntax (`[][]`) looks kind of odd, so we could rewrite the above interface like so:

```ts
interface Entry{
	...
	diagnosisCodes?: Array<Diagnosis['code']>;
}
```