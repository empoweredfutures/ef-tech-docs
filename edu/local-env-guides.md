# local environment guides

## initial setup of your local dev environment

- get the environment variables file from the [google drive](https://drive.google.com/drive/folders/1I5RhP9pw4k4I4CBjvbEn_1emIUOiY2qR) for the project you are working on
- rename the file from `<project-name>.env` to `.env`
- place this file in the root of the project it belongs to
- install docker
- `compose` the postgres database by right clicking the `postgres.docker-compose.yml` file and choosing `compose up`
- install node modules `npm i`
- `push` the current prisma schema to postgres with `npm run push`
- launch the nextjs dev server `npm run dev`
- seed the database with fake data

## seeding your database

- ensure that your database is running and the schema is pushed to it as described above
  - if the schema has changed recently you should reset your database or push the new schema to the database with "npm run push"
- run the nextjs dev server `npm run dev`
- navigate to http://localhost:3000/api/gql
  - if you get a 401 error please return to `/` and sign into the application with your EF google account
- on the left side toolbar click the folder icon
- where it says `add new` click the `Query` select element
- choose `Mutation` in the dropdown
- click the plus icon next to the select to create a new mutation
- a list of mutations will appear above
- click the `seed` mutation then click the pink play icon to run it
  - depending on the project you are on the `seed` mutation may have different names
- if you get back `true` then your database was seeded successfully

## resetting your database

whenever the prisma schema file changes your local database will need to be reset to reflect the changes

- stop / terminate the nextjs dev server and prisma studio if they are running
- right click the `postgres.docker-compose.yml` file
- select `compose restart`
- after the compose is finished run `npm run push` to push the prisma schema to the database
