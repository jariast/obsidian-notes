# 8.17 Listing Books
The books component was not working because the `author` field is now a separate model, we just have to change the query to this:

```js
export const ALL_BOOKS = gql`
  query AllBooks {
    allBooks {
      author {
        name
      }
      id
      published
      title
    }
  }
`;
```

Notice how the `author` field is now an object, we only need the `name` field of the Author so we only query for that field.

# 8.18 Login

We added a new `Login` component which is in charge of calling the mutation `LOGIN`, we decided to go with uncontrolled forms because we don't need to make any sort of validations, we just need to submit the user credentials.

In the `App` component we're using [[Custom Hooks#Custom Local Storage hook]] to save and retrieve the token from the local storage. We also added some guards to functionaliti

