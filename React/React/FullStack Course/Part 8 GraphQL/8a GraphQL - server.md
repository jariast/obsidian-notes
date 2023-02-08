Unlike REST APIs, Graph uses POST requests for all its operations. The browsers sends a Query to the de API, describing the required data.

## Schemas and queries

Schemas describe the data sent between client and server.
```js
type Person {
  name: String!
  phone: String
  street: String!
  city: String!
  id: ID! 
}

type Query {
  personCount: Int!
  allPersons: [Person!]!
  findPerson(name: String!): Person
}
```

The schema has two types, `Person` describes the object itself, it has 5 fields, the only optional field is phone.

The other type is `Query`. As with the Person type, exclamation marks denote which return types and parameters are Non-Null. We can use the queries like this:

```js
query {
	personCount
}
```

Assuming we have 4 persons, the response should look like this:

```js
{
  "data": {
    "personCount": 3
  }
}
```

For queries with parameters like the `allPersons` query, we must define which fields from the `person` schema to return:

```js
query {
  allPersons{
    name
    city
    street
  }
}
```

## Apollo Server

The current most popular library is Apollo server:

`npm install @apollo/server graphql`

The server is defined inside a `index.js` file. Inside the file we'll define the schema and the queries like shown above, we save those definitions in a variable like so:

```js
const typedDefs = glq`schema and queries go here`
```

Inside the file we also define `resolvers`, which is the code that defines how GraphQL queries are responded to.

```js
const resolvers = {
  Query: {
    personCount: () => persons.length,
    allPersons: () => persons,
    findPerson: (root, args) =>
      persons.find(p => p.name === args.name)
  }
}
```

## Mutations

All operation which cause a change are done with *mutations*. Example:

```js
type Mutation {
  addPerson(
    name: String!
    phone: String
    street: String!
    city: String!
  ): Person
}
```

If the operation succeeds, the new Person is returned, otherwise it returns null.
We must provide a *resolver* for the Mutation:

```js
const { v1: uuid } = require('uuid')

// ...

const resolvers = {
  // ...
  Mutation: {
    addPerson: (root, args) => {
      const person = { ...args, id: uuid() }
      persons = persons.concat(person)
      return person
    }
  }
}
```

