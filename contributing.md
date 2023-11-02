# Contributing

The current projects under development are:

- a rewrite of the mentorship platform (MP)
- an Android and iOS export of the MP
- the task management app (TMA)

To contribute to the projects in Empowered Futures, check out the Trello boards for the [Mentorship Platform](https://trello.com/b/U4Hb1AED/mentorship-platform-rewrite) and the internal [Task Management App](https://trello.com/b/eTfU1pUA/task-management-app). If you're not a member yet, the invite links are in the [onboarding instructions](https://github.com/empoweredfutures/ef-tech-docs/blob/main/onboarding.md).

You'll see a To-Do list. Feel free to add yourself to a card in the To-Do list (click on the card and add yourself as a member with the `join` button - or just hover over the card and press spacebar). Then move it the Doing list.

That's it - you can make a branch (see below) and get to work!

Before you get started, below are some key pre-requisites we all have to comply with before writing and submitting code.

## Editor Config

VSCode is the editor majority of the developers on the team are using and this document will assuming you are also using it.

You are welcome to use other editors but you'll have to figure out how to gain the same level of features covered here in your editor.

### Extensions

- [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

  - Provides a consistent code style for the project
  - Once installed edit your VSCode settings to format on save
  - `settings.json`:

  ```json
  {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
  ```

- [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

  - Provides additional intelligence to VSCode
  - Can find errors and enforces best practices
  - Some EF repos enforce that your code meet eslint and prettier checks to be committed, please ensure you follow what the linter recommends to you

- [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)

  - You'll need to run a postgres db for both the MP and the TMA. Docker is the easiest way to do that
  - Instructions for installing docker can be found on [docker's official docs](https://docs.docker.com/get-docker/)

- [GraphQL](https://marketplace.visualstudio.com/items?itemName=GraphQL.vscode-graphql)

  - Provides intelligence for graphql queries and mutations
  - GraphQL is now used within the MP and the TMA

- [TailWindCSS](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)

  - Provides auto-complete and linting for css classnames

- [GitHub PR's](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)
  - Makes it very easy to work with PR's, provides the ability to submit reviews and suggestions from within VSCode

## Interacting with GitHub

### Cloning

Once you have access to a repo you can clone it locally and start coding. Cloning can be done with the `git clone` command or with github desktop.

You'll need a `.env` file for the repos to run correctly, you can find these files on your EF google drive. You can find them under `Shared Drives > Technology & Innovation > Technology & Innovation Shared Space > env`.

### Branching

Once you're ready to make some changes you'll need to create a branch first.

VSCode provides git integration automatically: you can click the
git branch button in the bottom left and choose `Create new branch`

The branch naming convention for both backend and frontend is
`MMDD-<meaningful-name>`.

Once a branch is created you can safely commit to it, **never commit to main directly - always commit to your own branch**.

When you're ready to push your code to the remote repo, your command should look something like this:

```
git push origin 0623-add-widget-feature
```

### Making a PR

When you're finished with your ticket you can then open a Pull Request on github.

Opening the repo's github page in a browser after committing will show a button to quickly make a PR with your branch, you can also make a PR directly in VSCode if you have the extension installed.

Naming the PR the same name as the branch is acceptable if the branch name is meaningful enough.

You should also write a description for your PR and provide additional info (such as links to design pages or trello tickets) to help reviewers understand your work / changes, if your PR depends on another PR or a backend change be sure to make note of this.

Take advantage of the many labels available on the GitHub repo to add descriptors such as `needs reviewer`, `not ready yet`, or `dependency` to provide quick information to reviewers.

Once you've posted your PR for review feel free to notify other devs on slack with a link to get some eyes on your work.

### Merging a PR

If your branch is out of date with `main` or if you have merge conflicts you'll need to pull the `main` branch into with yours and resolve conflicts.

Pay close attention when resolving conflicts as it's possible that you may overwrite or undo a teammates work.

You must receive 2 approvals from teammates to merge your PR to `main`.

You are not allowed to be a reviewer on a PR that you have worked on / committed to, exceptions can be made if your contributions are small or negligible.

Anyone on the team is allowed to merge a PR if the PR has 2 approvals.

When merging it is preferred that you use github's `squash and merge` function to keep the number of commits on the `main` branch low.
