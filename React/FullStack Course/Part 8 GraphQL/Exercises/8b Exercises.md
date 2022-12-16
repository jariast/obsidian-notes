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