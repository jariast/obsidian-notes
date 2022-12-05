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

