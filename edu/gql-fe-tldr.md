# GraphQL FE TLDR

this page quickly details how graphql works on the client in contrast to standard rest apis

### Queries

getting a list of users and their tasks:

REST:

```tsx
const [users, setUsers] = useState<User[]>([])
useEffect(() => {
  axios
    .get<User[]>('/api/users')
    .then((res) => setUsers(res.data))
    .catch(console.error)
}, [])
```

- does not have error or loading states
- over-fetches user data, it's not likely that every property on the user is needed for this component
- related data is needed (each users tasks) but cannot be returned from `/api/users`
- logs the full error to the client, could contain sensitive information, does not show the user anything went wrong

with this approach you get all information about the users but it is still missing the data you actually need for this component, each users tasks, it's over-fetching and under-fetching simultaneously

to then get the users tasks with this approach you'd have to map over every user and issue another `axios.get` request for their tasks

- creates a waterfall of requests on the client
- requires even more `useState` and `useEffect`
- will very likely over-fetch the users tasks as well
- overall this is `On+1`, where `n` is the number of users

GraphQL:

```tsx
const [res, refresh] = useQuery({
  query: gql`
    {
      users {
        id
        name
        email
        picture
        tasks {
          id
          name
          description
          status
          priority
        }
      }
    }
  `,
})
```

- fetches exactly what is required for the component or page, no more or less
- related data is not fetched in `On+1` time on the client, the client makes less requests to the backend, transfers less data, and sees results faster
- the frontend code has this `gql` string, frontend developers can easily see what data is being returned from the backend, they can add or remove properties from the string as the components grows or shrinks
- the `gql` string will always match the returned JSON shape
- `data`, `error`, and `loading` states are all included in the `res` object
- stores data in a memory cache that is available globally to all components

all data will need to be relational to some extent in any application, gql exists because there needed to be a way to programmatically and dynamically query this data

---

### Mutations

creating a task:

REST:

```tsx
function createTask() {
  axios
    .post(
      '/api/tasks',
      { name, description },
      { headers: { Authorization: `bearer ${accessToken}` } },
    )
    .then((res) => {
      setSuccess(true)
      setError(false)
    })
    .catch((e) => {
      console.error(e)
      setSuccess(false)
      setError(true)
    })
}
```

- need to manually have states for error and success
- not clear on what response / HTTP code the backend will return
- calling multiple `setState`'s at once will cause multiple renders
- data being sent is not validated or typed
- `accessToken` is manually injected into the request header rather than being handled at a higher level or elsewhere automatically

GraphQL:

```tsx
const [res, createTask] = useMutation(gql`
  mutation ($name: String!, $description: String) {
    createTask(name: $name, description: $description)
  }
`)
```

- clear what data is needed and what type
- required data is marked with a `!`
- clear on what response is returned (just a boolean here)
- `res` object again includes `loading`, `error` and, `data` states
- user auth is handled elsewhere, rather than in the request body itself

gql takes care of data validation on all queries and mutations, this is normally something that has to be manually done in a REST api

gql will also return readable errors if data sent is not the correct type, another thing that must be handled manually in REST
