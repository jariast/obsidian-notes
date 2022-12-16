# Apollo Client initial setup.

We can follow the documentation [guide](https://www.apollographql.com/docs/react/get-started/)

- Run `npm install @apollo/client graphql`
- Import dependencies on `index.js`.
- Instantiate new `ApolloClient`:
 ```js
 const client = new ApolloClient({
  cache: new InMemoryCache(),
  link: new HttpLink({
    uri: 'http://localhost:4000',
  }),
})
```
- Wrap `App` component with `ApopploProvider`.
- Create `queries` file.

The Apollo Explorer is really useful for creating the queries, we can create the queries there and paste them on our code.

# 8.8 Authors view

We used destructuring when we call the query:

```js
const { data, loading } = useQuery(ALL_AUTHORS);
```
 That way we have easy access to `data` and `loading`, we can also use it to obtain the `error` field if needed.

# 8.10 Adding a book

In order to keep the Authors and Books views updated, we used refetching queries as seen on [[8b React and GraphQL#Updating cache]].

# 8.11 Author's birth year

As the next exercise invalidates the possibility of updating a non-existing author, we don't have to take into consideration the issue raised on [[8b React and GraphQL#Updating objects]]

