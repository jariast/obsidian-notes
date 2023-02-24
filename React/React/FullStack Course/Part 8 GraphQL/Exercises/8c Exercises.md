# Setup
#backendSetup #security #environment #packages

- Install mongoose
``` bash
npm install mongoose
```

- Install [dotenv](https://github.com/motdotla/dotenv)
```bash
npm install dotenv --save
```

- Install [cross-env](https://www.npmjs.com/package/cross-env) for Windows compatibility.

```bash
npm install --save-dev cross-env
```

We add a `.env` file with the DB URI and the App secret. Remember to add the this file to `.gitignore`.

We must call `require('dotenv').config()` in the `app.js` file to ensure that the variables setup in `.env` file are available.

In `package.json` we modified the scripts like this:

```json
"dev": "cross-env NODE_ENV=development nodemon index.js"
```


# 8.13: Database, part01

I was facing a bug when changing the queries from arrays to using the DB, I forgot to use the `async` keyword in the start of the function.

It was really crucial to understand that the Author was no longer a String and it is indeed another entire schema, so when Adding a New Book, we needed to add the Author's ID to the Book object and not just its name or  any other object.

# 8.14: Database, part 2

When implementing the parameters for the `allBooks` query,  I was facing the issue of dealing with the optional parameters. Mongoose queries require a value for a filter:

```js
db.inventory.find( { status: "D" } )
```

So I came up with a `queryObject` that will only add the filter fields if they were provided by the request.

```js
 allBooks: async (__, { authorName, genre }) => {
      const author = await Author.findOne({ name: authorName });
      const queryObject = {};
      author ? (queryObject.author = author.id) : null;
      genre ? (queryObject.genres = genre) : null;
      return Book.find(queryObject);
    },
```

#reviewSolutionAfterSubmission 

# 8.15 Database, part 3

#courseMaterialCorrection 

As the exercises in [[8a Exercises#Apollo Server Issues]] the newer versions of Apollo Server don't [expose](https://www.apollographql.com/docs/apollo-server/migration#built-in-error-classes) the `UserInputError` classes. Instead we must use the newer `GraphQLError` class to throw [Custom Errors](https://www.apollographql.com/docs/apollo-server/data/errors/#custom-errors). 

In the previous exercise, I forgot to implement a way for the `allBooks` query to return the Author's info. Surprisingly for me, using Mongoose's `populate` method was enough to return the Author's info, including the `bookCount` field.

Maybe it shouldn't be so surprising, considering that Apollo automatically resolves the `__id` field to to `id`.

# 8.16 User and logging in

#packages 

```bash
npm install jsonwebtoken
```

Way trickier than expected.

The issue began with this code from the course:

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

As stated in the [documentation](https://www.apollographql.com/docs/apollo-server/migration/#context-initialization-function) in V4 the context can no longer be initialized in that way. Besides that, the `jwt.verify` method will error out if we provide an invalid token, breaking the Apollo explorer (it will say something like "The introspection query didn't work").

The user authentication [[8c Database and User Administration#User and Login]] implementation works just fine, but in my opinion it's a little bit wasteful, because it seems like the context function is ran every single time a request is made to the server. 

I chose to in the context only extract the token from the header, if a request requires authentication, it can run the whole flow itself.

As seen on the previous exercises, we need to use the new `GraphQLError` to throw errors, the authentication error has an extra option for changing the http status.

```js
throw new GraphQLError('User is not authenticated', {
      extensions: {
        code: 'UNAUTHENTICATED',

        http: { status: 401 },
      },
    });
```