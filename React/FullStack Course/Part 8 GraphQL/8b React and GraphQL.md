# Setup
We could directly use GraphQL by sending POST request to the backend, but that would be really cumbersome.

We'll use [Apollo Client](https://www.apollographql.com/docs/react/) to make our requests from React.
We must install the dependencies in our React project:

```bash
npm install @apollo/client graphql
```

Apollo uses the `client` object to communicate with the GraphQL server. In order for the components to be able to use the client, we must wrap the `App` component in `AppProvider`

```jsx
<ApolloProvider client={client}>
	<App />
</ApolloProvider>
```

# Querying
The most common way to query is using [useQuery](https://www.apollographql.com/docs/react/api/react/hooks/#usequery) hook. When the query is called, it returns and object with multiple fields, when the server hasn't responded to the request the `loading` field is set to `true`. 

When a response is completed and we receive data, we can find it in the `data` field.

# Queries and variables
In order to use queries without hard-coded data, we must pass variables to them. To pass variables, we must *name* our queries.

```js
query findPersonByName($nameToSearch: String!) {
  findPerson(name: $nameToSearch) {
    name
    phone 
    address {
      street
      city
    }
  }
}

```

By default, `useHook` is called as soon as the component is *rendered*, if we want to run the query only when a condition is met we can use the `skip` option:

```js
const result = useQuery(FIND_PERSON, {
    variables: { nameToSearch },
    skip: !nameToSearch,
  })
```
 Above, the query will *skip* its execution if `nameToSearch` is falsy.

# Cache

Apollo client saves the responses of queries in cache. If the response to a query is already in cache, the query is not sent to the server.

# Mutations

Like Queries, we need to name our Mutations in order to use variables. We use the `useMutation` hook:

```js
const [ createPerson ] = useMutation(CREATE_PERSON) // Initializing the component
...
createPerson({  variables: { name, phone, street, city } }) // Used inside Submit handler for example
```

After the mutation is run, the application is not automatically updated because the cache hasn't been updated. For example, we have the list of persons that uses a query to retrieve all the persons, once we run the mutation, the cache still has the same Persons info.