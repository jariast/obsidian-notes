
# Mongoose and Apollo

We're gonna use Mongoose again to manage the DB connection. The DB schemas are the same structure as before, but we'll make sure to set to `required` the same fields that are required in the GraphQL schema, just to be safe.

Most of the code is the same as before, the *types* definitions stay the same, the biggest changes are in the `resolvers`. As the DB operations are `promises`, the resolvers should return an `async` function, Apollo takes care of returning the value once the promises complete.

```js
Mutation: {
    addPerson: async (root, args) => {
      const person = new Person({ ...args })
      return person.save()
    },
    editNumber: async (root, args) => {
      const person = await Person.findOne({ name: args.name })
      person.phone = args.phone
      return person.save()
    },
  },
```

GraphQL also parses the `_id` field of the Mongo objects to `id` automatically.

# Validation

We can use a `try/catch` block to handle errors thrown by Mongoose:

```js
addPerson: async (root, args) => {
      const person = new Person({ ...args });

      try {
        await person.save();
      } catch (error) {
        throw new UserInputError(error.message, { invalidArgs: args });
      }
      return person;
    }
```

# User and Login

The users are handled the same way as on [Part 04](https://fullstackopen.com/en/part4/token_authentication) of the course. In the course's example they're using the same hardcoded password for simplicity purposes, so when a user tries to login, the `login` mutation checks that the password equals "secret". 

We need to "protect" some of our Queries, so only logged users can access them, when we need to run code that is shared by multiple resolvers, we should use the `Context` parameter of a server Instance:

```js
const server = new ApolloServer({
  typeDefs,
  resolvers,
  context: async ({ req }) => {
    const auth = req ? req.headers.authorization : null;
    if (auth && auth.toLowerCase().startsWith('bearer ')) {
      const decodedToken = jwt.verify(auth.substring(7), JWT_SECRET);
      const currentUser = await User.findById(decodedToken.id).populate(
        'friends'
      );
      return { currentUser };
    }
  },
});
```

The above `context` function returns and object with the `currentUser` field set to the user found in the DB. Queries that need to access the logged user, can access it like this:

```js
Query: {
  // ...
  me: (__, __, context) => {
    return context.currentUser
  }
},
```

If no user is found we can throw an Authentication Error:

```js
if (!currentUser) {
	throw new AuthenticationError('not authenticated');
}
```