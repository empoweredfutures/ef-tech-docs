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
