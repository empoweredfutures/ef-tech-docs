# Troubleshooting

## Docker

check the your user has permission to use docker commands, if you are on linux you will likely need to follow the [post install steps](https://docs.docker.com/engine/install/linux-postinstall/)

check that you have the [vscode docker extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker), this will help you manage your containers and cleanup unused volumes

if docker is still not working try re-installing it / updating it,

you'll know when your docker is working correctly when:

- the vscode docker tab shows you info about your docker install
- running `docker version` on your cli returns successfully with the latest version info
- running `docker run hello-world` on your cli returns successfully

## Postgres

it is recommended that you [reset your database](../local-env-guides.md#resetting-your-database) every time you develop to ensure that you always have a clean db that is synced with the latest changes to the schema

if your issue is that you cannot connect / push to the database try changing your `.env` files `DATABASE_URL` variable, change the `user` in the url to your username on your machine, this has been found to be the case on certain MacOS machines

## Unable to Commit

our projects use a tool called `husky` to ensure files committed to our repos meet certain standards

`husky` is a tool that has "hooks" that hook into git commands, when you run `git commit` you are calling the husky `pre-commit` shell script from the `.husky` folder

this script then calls another tool called `lint-staged` which will run any command you specify against files that are currently in the staging area of git

`lint-staged` currently runs both `eslint` and `prettier` checks on your staged files, if it finds an error or warning it will not allow the original `git commit` command to complete

this type of check is different from the one we have on github that tests our builds, this instead checks that only `eslint` and `prettier` are passing, this means that your file could have a type error or a build error and it will still pass this check

the easiest way to fix this error is to check the error message and see what files caused the error, open the file in your editor and it will mark the error/warning for you in red or yellow underlines (using the eslint extension)

if it's a prettier error a simple fix is to run `prettier -w <path to file>`

this may be a sign that your editor is not setup to format your code on save using the prettier extension, it's strongly recommended that you do this to avoid prettier errors in the future, add this to your vscode's settings.json file

```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode"
}
```

## 401 Unauthorized

in almost all cases this is caused by not having a valid auth session in the application

most commonly happens when `/api/gql` is visited before logging into the application on the homepage

it can also happen when you've reset your database and your previous session is no longer valid

in all cases it can be fixed by visiting the homepage and signing in with your google account

## GQTY:GEN ES Module error

this is a known issue effecting gqty's generate command, to fix it follow these steps:

- remove the `prettier.config.js` file
- inside the `node_modules` folder remove the `prettier` folders
  - prettier
  - prettier-plugin-tailwindcss
  - prettier-plugin-organize-imports
- run the `gqty:gen` script (`npm run gqty:gen`)

once the `gqty:gen` script executes successfully you can restore the prettier config and folders either from your machines bin or using git (for the config) and `npm i` to reinstall the prettier node_modules folders
