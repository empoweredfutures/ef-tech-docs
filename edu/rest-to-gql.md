# REST to GraphQL

lets say we're building a task management app like trello, we'll need a way to save tasks and have users join tasks as assignees

we can say that a task can have many users and a user can have many tasks, in prisma it'll look like this (omitting fields here for brevity)

```prisma
model User {
  tasks Task[]
}

model Task {
  assignedTo User[]
}
```

since REST typically follows convention we can assume that:

- GET /user returns a list of users
- GET /user/:id returns a specific user

and the same for the `Task` endpoints also

immediately a problem is apparent, what if we need show all tasks for a specific user, like for a dashboard; or what if we want to show what users are working on a task when viewing a single task

one quick fix is to add a query param that handles this

```ts
function getTask(id) {
  return req.query.withUsers ? getTaskWithUser(id) : getOnlyTask(id)
}
```

while this does fix the problem, it leads us to another problem. this fix won't scale well as more relationships and models are created to make the app more feature complete

lets add a model called `Team` that tracks members and tasks

```prisma
model Team {
  members User[]
  tasks   Task[]
}
```

then update the `getTask` call to allow getting the related data

```ts
function getTask(id) {
  return req.query.withUsers ? getTaskWithUsers(id) : getOnlyTask(id)
  return req.query.withTeams ? getTaskWithTeams(id) : getOnlyTask(id)
}
```

this will only get more and more problematic as relationships grow. it also creates a situation in which both users and the teams cannot both be fetched together on a task

you may think that "the client should not ever need to get both of those in this way", but what's important to remember is that, as a backend developer, we should not make decisions that limit the frontend developers options

this api, just like libraries like express and react, are meant to be as open-ended as possible to allow for users to use it in any way they want

enter graphql (gql):

```gql
type Query {
  users: [User!]!
  user(id: String!): User!
  tasks: [Task!]!
  task(id: String!): Task!
}
```

gql needs a schema, which can be written in it's own schema language that is very similar to prisma's schema language, allowing for very similar looking files, which makes it easier to map data from the sql database to the gql api

you can re-use the same type definitions as seen in the prisma code-blocks above for the gql `User`, `Task`, and `Team` types

one notable difference is that fields _not_ re-declared in the gql schema **will be ignored** even if they are present in the prisma schema, this is useful for cases where you want to hide / protect information from the api, such as a password field

here is what a query looks like for the dashboard ui problem as described above, this will get all data needed for getting a specific user's tasks, then rendering the task with info about who's on the task as well

```gql
query ($id: String!) {
  user(id: $id) {
    name
    picture
    tasks {
      id
      title
      description
      assignedTo {
        id
        name
        picture
      }
    }
  }
}
```

you can see here that you can "nest" into related fields as if they were a simple javascript object, graphql will then grab that related data for you (explained below) and return it in a single request

this solves the problem of fetching multiple relations in one request, it also solves a side-effect of REST apis "over-fetching"

typically when you GET from `/task/:id` it will return the **entire** task object from the db, meaning all fields on the task in the db row, this problem cascades when you consider `withUsers` is possible

REST could return hundreds of kilobytes to the client in situations where only a small portion of the returned data is needed for the client app to function / render

in the gql query above you can see that only some fields from the models are specified, this tells the gql server what the client actually needs, gql then trims the object internally and sends the JSON response with only the data + fields requested

how does graphql know how to fetch the related data?

```ts
const resolvers = {
  Query: {
    Task: {
      users: async function (parent: Task) {
        const task = await prisma.task.findUnique({
          where: { id: parent.id },
          select: { users: true },
        })

        return task.users
      },
    },
  },
}
```

here we see one related data resolver, this tells the gql server how to get `users` for a task, when it only knows the task id

this is certainly tedious to manually implement for every related field on every model, so we make use of a library called `pothos` that automatically fetches related data from prisma with it's prisma plugin

the `pothos` plugin shows the full power that gql can provide by **generating sql queries at request time**, this removes the On + 1 problem that many gql servers can be burdened by

---

when it comes to other operations in REST like POST, PUT, DELETE gql has Mutations

there is not much to say on graphql mutations however as they are very similar to what you'd likely find in REST

```gql
type Mutation {
  createTask(title: String!, description: String): Task!
}
```

```ts
const resolvers = {
  Mutation: {
    createTask: async function (parent, args) {
      const { title, description } = args
      const task = await prisma.task.create({
        data: { title, description },
      })
      return task
    },
  },
}
```

here is a simple create function, it's likely that in REST it would look somewhat similar, though with more boilerplate to verify and parse the incoming data

it's important to know that in gql its customary to return the type that the mutation mutates, so `createTask` would return `Task`, and `updateUser` would return `User` etc...

you'll also notice that since the return type is `Task` even mutations can return related data

```gql
mutation ($title: String!, $description: String) {
  createTask(title: $title, description: $description) {
    id
    assignedTo {
      id
      name
    }
  }
}
```

one of the reasons why the return type must be the same type as the one being mutated is due to frontend caching, by default frontend react clients like urql will cache all queries

when the `createTask` mutation is called the client will be intelligent enough to know that a mutation was just called on `Task`, and it will automatically invalidate the cache with the task id that is returned

---

other benefits that gql include are:

- automatic data-validation for both incoming and outgoing data
- the gql schema provides complete documentation for the entire api
- custom data validators for special types like `DateTime` (via packages / addons)
