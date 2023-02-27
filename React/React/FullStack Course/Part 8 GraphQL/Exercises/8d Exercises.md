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

