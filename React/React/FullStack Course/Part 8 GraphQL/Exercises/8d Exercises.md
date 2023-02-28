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

In the `App` component we're using [[Custom Hooks#Custom Local Storage hook]] to save and retrieve the token from the local storage. We also added some guards to functionalities like Adding a Book so only logged in users can access that page.

## Auth Header
#auth
When creating the headers in the React App I was getting the token from `localStorage` and directly adding it to the the auth string, this resulted in the token having Quotation marks at the start and end, which made the validation fail.

I fixed the issue by Parsing the token before adding it to the header:

```js
const token = JSON.parse(localStorage.getItem('books-app-user-token'));
```
