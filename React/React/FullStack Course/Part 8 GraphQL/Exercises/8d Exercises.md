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

# 8.19 Books by genre pt 1
We had to modify the `Books` component to show a list of Filters on all the genres, as we don't have a Genres query we must build the list using the info we have in the Books array.

```js
function extractGenres(books = []) {
    const bookGenres = books.map((book) => book.genres).flat();
    const uniqueGenres = [...new Set(bookGenres)];
    return uniqueGenres;
}
  ```

The more interesting part of the code happens when we try to remove the duplicate Genres from the array, we use a `Set` constructor to convert the `bookGenres` array into a Set, the Set object won't allow for duplicate keys, we then convert back the Set to an array using `spread` syntax.

8.20 Books by genre pt 02

We implemented a new component that shows the books filtered by the Logged In user's Favorite Genre.

The component is very similar to the `Books` component, this certainly points to writing some new smaller more specialized components like `Table` and `Filter`. 

As the query for getting the user's info requires that an user has actually to be logged in, we used the `skip` option of the `useQuery` hook:

```js
  const { data, loading } = useQuery(GET_USER_INFO, { skip: !token });
```

We're passing to the component the `token` prop when a user is Logged In, if there's no token the query will be skipped and once we log in, we'll actually make the query. At this point we were getting a strange behavior when we were logging in, the query will be sent without the `auth` header present, causing it to fail. The culprit was this piece of code in our 