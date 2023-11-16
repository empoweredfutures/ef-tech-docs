# local environment guides

## initial setup of your local dev environment

- get the environment variables file `.env` from the [google drive](https://drive.google.com/drive/folders/1I5RhP9pw4k4I4CBjvbEn_1emIUOiY2qR)
- install docker
- `compose` the postgres database by right clicking the `postgres.docker-compose.yml` file and choosing `compose up`
- install node modules `npm i`
- `push` the current prisma schema to postgres with `npm run push`
- launch the nextjs dev server `npm run dev`
- (optional) seed the database with fake data [see here](#seeding-your-database)

## seeding your database

- ensure that your database is running and the schema is pushed to it as described above
  - if the schema has changed recently you must reset your database [see here](#resetting-your-database)
- run the nextjs dev server `npm run dev`
- navigate to http://localhost:3000/api/gql
- on the left side toolbar click the folder icon
- where it says `add new` click the `Query` select element
- choose `Mutation` in the dropdown
- click the plus icon next to the select to create a new mutation
- a list of mutations will appear above
- depending on the project you are on the `seed` mutation may have different names
- click the `seed` mutation then click the pink play icon to run it
- if you get back `true` then your database seeded correctly

## resetting your database

whenever the prisma schema file changes your local database will need to be reset to reflect the changes

- stop / terminate the nextjs dev server and prisma studio if they are running
- right click the `postgres.docker-compose.yml` file
- select `compose restart`
- after the compose is finished run `npm run push` to push the prisma schema to the database
- (optional) seed the database with fake data [see here](#seeding-your-database)
