
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