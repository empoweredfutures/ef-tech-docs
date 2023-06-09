# Contributing

This page details key pre-requisites to comply with before writing and submitting code

## Editor Config

VSCode is the editor majority of the developers on the team are using and this document will assuming you are also using it

you are welcome to use other editors but you'll be on your own for figuring out how to gain the same level of features covered here in your editor

### Extensions

- [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

  - Provides a consistent code style for the project
  - Once installed edit your VSCode settings to format on save
  - `settings.json`:

  ```
  {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode",
  }
  ```

- [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

  - Provides additional intelligence to VSCode
  - Can find errors and enforces best practices
  - Some EF repos enforce that your code meet eslint and prettier checks to be committed, please ensure you follow what the linter recommends to you

- [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)

  - You'll need to run a postgres db for both projects and docker is the easiest way to do that
  - Instructions for installing docker can be found on [docker's official docs](https://docs.docker.com/get-docker/)

- [GraphQL](https://marketplace.visualstudio.com/items?itemName=GraphQL.vscode-graphql)

  - Provides intelligence for graphql queries and mutations
  - GraphQL is currently used only within the internal task management app

- [TailWindCSS](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)

  - Provides auto-complete and linting for css classnames

- [GitHub PR's](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)
  - Makes it very easy to work with PR's, provides the ability to submit reviews and suggestions from within VSCode

## Interacting with GitHub

### Cloning

Once you have access to a repo you can clone it locally and start coding. Cloning can be done with the `git clone` command or with github desktop

You'll need a `.env` file for the project to run correctly, you can find these files on slack in the `pinned` messages, check `#backend` for the main project's `.env` and check `#internal-project` for the task management app's `.env` file

`.env` files are typically only for backend repos but in the case of the internal project, both the backend and frontend are a single repo

### Branching

Once you're ready to commit changes you'll need to create a branch

VSCode provides git integration automatically, you can click the
git branch button in the bottom left and choose `Create new branch`

The branch naming convention for both backend and frontend is
`MMDD-<meaningful-name>`

Once a branch is created you can safely commit to it, **never commit to main / development directly, always commit to your own branch**

### Making a PR

When you're finished with your ticket you can then open a Pull Request on github

Opening the repo's github page in a browser after committing will show a button to quickly make a PR with your branch, you can also make a PR directly in VSCode if you have the extension installed

Naming the PR the same name as the branch is acceptable if the branch name is meaningful enough

You should also write a description for your PR and provide additional info (such as links to design pages or trello tickets) to help reviewers understand your work / changes, if your PR depends on another PR or a backend change be sure to make note of this

Take advantage of the many labels available on the GitHub repo to add descriptors such as `needs reviewer`, `not ready yet`, or `dependency` to provide quick information to reviewers

Once you've posted your PR for review feel free to notify other devs on slack with a link to get some eyes on your work

### Merging a PR

If your branch is out of date with `main` or if you have merge conflicts you'll need to pull the `main` branch into with yours and resolve conflicts

Pay close attention when resolving conflicts as it's possible that you may overwrite or undo a teammates work

You must receive 2 approvals from teammates to merge your PR to `main`

You are not allowed to be a reviewer on a PR that you have worked on / committed to, exceptions can be made if your contributions are small or negligible

Anyone on the team is allowed to merge a PR if the PR has 2 approvals

when merging it is preferred that you use github's `squash and merge` function to keep the number of commits on the `main` branch low
