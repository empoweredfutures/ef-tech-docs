# GQTY

the gqty lib allows FE devs to write plain typescript code and then have the lib automatically generate the gql needed to fetch the data from the BE

## Queries

here is how you would fetch a user and their name with a normal gql query

```gql
query GetUserName($userId: String!) {
  user(id: $userId) {
    name
  }
}
```

now the problem is that this gql query is just a plain string in typescript, if you pass it to `Urql.useQuery` urql will not know what type it returns, thus typescript cannot help with typechecking

one way to solve this problem is to setup graphql-codgen, in the case of the mp-rw this was setup, however the setup was less than ideal

for gql-codegen to function you must:

- install multiple dependencies (200 total)
- setup where your queries and mutations are
  - these are hard-coded and all have unique names, not very flexible
- re-run the codegen every time any part of any query or mutation changes
  - if you add or drop a single field you'd have to run it all over again

as you can see that's alot of negatives, but it was worth it overall for the typesafety and ease of development it initially provided

that is of course until the GQTY lib was known to me, this lib generates code just like the gql-codegen, but only for the schema, it then allows you to write typescript code using this schema, the code is reviewed by GQTY during the react render and only then is a gql query made

here is the same gql query as above but with gqty and typescript

```tsx
const query = useQuery()
const user = query.user({ id: userId })
const name = user.name
```

when this component renders gqty will generate a query that looks almost just like the one above automatically

this has the added bonus that you can then ask for more data and the query that fetches that data will grow as you use more fields

```tsx
const tasks = query.tasks({ take: 20 })

return (
  <div>
    {tasks.map((task) => {
      return (
        <div key={task.id ?? 0}>
          {task.name}
        <div>
      )
    })}
  </div>
)
```

this code will generate a query like

```gql
query {
  tasks(take: 20) {
    id
    name
  }
}
```

if you later add another field the query auto updates

```tsx
<div key={task.id ?? 0}>
  {task.name}
  {task.description}
<div>
```

```gql
query {
  tasks(take: 20) {
    id
    name
    description
  }
}
```

you may have noticed the `key={id ?? 0}`, this is a qwirk of gqty, when using ids as keys you have to provide a default in case the data is not there yet

---

gqty also allows for easier types when passing data from one component to another

in gql-codegen a query like

```gql
query User($id: String!) {
  name
}
```

would generate a specific type like

```ts
type UserQueryData = {
  name: string
}
```

that looks okay until you need to pass data to a child component

```tsx
function myChildComp(props: { user: User }) {}
```

the `UserQueryData` type only has the name field so typescript won't allow it to be passed to the `User` type, even though it's technically the same type

in gqty you can just specify `User` and it will work

---

lastly, and most importantly, gqty merges multiple queries into one, thus making the application more efficient and faster to load

if 2, or 3, or even 20 components all render at once, and all call the `useQuery` hook, gqty will merge them all into a single api call

this ability to ask for everything at once is one of the reasons why GraphQL was created but is difficult to actually pull of in a complex and modular application, gqty allows for this with great ease

example:

```tsx
function Main() {
  const query = useQuery()
  const currentUser = query.my
  const myName = currentUser.name
  const myRole = currentUser.role

  return (
    <>
      <p>
        {myName} - {myRole}
      </p>
      <MentorList />
    </>
  )
}

function MentorList() {
  const query = useQuery()
  const mentors = query.users({ filter: { role: 'Mentor' } })

  return (
    <>
      {mentors.map((mentor) => (
        <MentorCard mentor={mentor} />
      ))}
    </>
  )
}

function MentorCard({ mentor }: { mentor: User }) {
  return (
    <>
      <img src={mentor.picture} />
      <div> {mentor.name} </div>
      <div> {mentor.title} </div>
    </>
  )
}
```

all of that will compile into a single query

```gql
query {
  my {
    name
    role
  }
  users(filter: { role: "Mentor" }) {
    picture
    name
    title
  }
}
```

## Mutations

the syntax for writing a mutation is strange with gqty

```tsx
const [mutate, mutateRes] = useMutation(
  (mutation, args: MutationArgs<'updateUser'>) => {
    const user = mutation.updateUser({ name: args.name })
    return user.id // you MUST return something from the response, the id is a common choice
  },
)
```

the `mutate` var is the function that calls the function passed to the `useMutation` call, the args parameter is not typed by default, the `MutationArgs` type is a helper type to infer what the args should be

if you're wondering why it isn't typed even though we can infer the type, it is strange choice by the gqty team but it does allow for optionally not not providing an `args` parameter at all

```tsx
const [role, setRole] = useState<UserRole>()
const [mutate, mutateRes] = useMutation((mutation) => {
  const user = mutation.setOwnRole({ role: role })
  return user.id
})
mutateRes.data
//        ^? string
```

here no `args` is given allowing `mutate` to be called with no parameters, the needed variables are already referenced inside the mutation function

`mutateRes` is a stateful variable also, it has `data`, `error`, and `loading` states. the main difference from other gql clients is that the `data` is dynamically typed by what you choose to return from your mutation callback, in the examples above `mutationRes.data` would be a string as `User.id` is a string

```tsx
const [mutate, mutateRes] = useMutation((mutation) => {
  const user = mutation.setOwnRole({ role: role })
  return {
    id: user.id,
    role: user.role,
  }
})
mutateRes.data
//        ^? { id: string, role: UserRole }
```

you can return any shape you want from the mutation callback just remember to include (select) at least one property from the type that is returned

---

for more info please see the gqty docs at https://gqty.vercel.app/
