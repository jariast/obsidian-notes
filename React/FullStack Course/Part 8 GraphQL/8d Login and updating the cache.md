# Login

Login mutation:
```js
export const LOGIN = gql`
  mutation login($username: String!, $password: String!) {
    login(username: $username, password: $password)  {
      value
    }
  }
`
```

We use the mutation like this:
```js
const [login, result] = useMutation(LOGIN, {
    onError: (error) => {
      setError(error.message);
    },
  });

  useEffect(() => {
    if (result.data) {
      const token = result.data.login.value;
      handleLogin(token);
    }
    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, [result.data]);
  
```

# Authenticating Requests

We must add the toke provided by the login operation to all the requests that require authentication. Snippet of code taken from Apollo Client [docs](https://www.apollographql.com/docs/react/networking/authentication/):

```js
import { ApolloClient, createHttpLink, InMemoryCache } from '@apollo/client';
import { setContext } from '@apollo/client/link/context';

const httpLink = createHttpLink({
  uri: '/graphql',
});

const authLink = setContext((_, { headers }) => {
  // get the authentication token from local storage if it exists
  const token = localStorage.getItem('token');
  // return the headers to the context so httpLink can read them
  return {
    headers: {
      ...headers,
      authorization: token ? `Bearer ${token}` : "",
    }
  }
});

const client = new ApolloClient({
  link: authLink.concat(httpLink),
  cache: new InMemoryCache()
});
```