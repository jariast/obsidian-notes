# 8.1 Number of books and authors

## Apollo Server Issues

 I was having issues with the import: 
```js
const { ApolloServer, gql } = require('@apollo/server');
```

The app was throwing that `gql` is not a function, had to dig into the [Documentation](https://www.apollographql.com/docs/apollo-server/migration/#gql-graphql-tag) and found that on Apollo Sever V4 `gql` was no longer exported by Apollo.

In order to fix the issue, we must remove the import from Apollo Server, install [gql-tag](https://www.npmjs.com/package/graphql-tag) and import `gql`

