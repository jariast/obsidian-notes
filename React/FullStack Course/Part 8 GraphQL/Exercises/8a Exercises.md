# 8.1 Number of books and authors

## Apollo Server Issues

### gql Tag

#courseMaterialCorrection
 I was having issues with the import: 
```js
const { ApolloServer, gql } = require('@apollo/server');
```

The app was throwing that `gql` is not a function, had to dig into the [Documentation](https://www.apollographql.com/docs/apollo-server/migration/#gql-graphql-tag) and found that on Apollo Sever V4 `gql` was no longer exported by Apollo.

In order to fix the issue, we must remove the import from Apollo Server, install [gql-tag](https://www.npmjs.com/package/graphql-tag) and import `gql`

### Apollo Server Standalone

#courseMaterialCorrection 
In Apollo V4 we must use `startStandaloneServer` in order to create an instance. See [Apollo Migration](https://www.apollographql.com/docs/apollo-server/migration/#migrate-from-apollo-server)

Apollo V3:

```js
server.listen().then(({ url }) => {
  console.log(`Server ready at ${url}`);
});
```

Apollo V4:

```js
const { url } = await startStandaloneServer(server, {
  listen: { port: 4000 },
});

console.log(`🚀  Server ready at: ${url}`);
```

The above code only works for ES Modules, and we would need to add the following declaration to `package.json`. 

```json
{
	"type": module
}
```

In the course we're using Common JS modules, the `await` syntax won't work with these types of modules, so we must use the old Promise syntax:

```js
startStandaloneServer(server, {
  listen: { port: 4000 },
}).then(({ url }) => {
  console.log(`Server ready at ${url}`);
});
```

## Queries

The queries are pretty straightforward, we only need to implement the queries types. The Book or Author types are not required for either of these queries, because they will only return an Int type.

# 8.3 All Authors

The exercise calls for the query to be able to return `bookCount` field, so we must add that field to the Author schema, since the Object stored in our arrays don't have that field, we must write a resolver for it.

I think that resolver is a good place to practice Functional Programming. #TODO #functional
