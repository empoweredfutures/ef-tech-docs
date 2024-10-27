# Contributing

This page details steps to setup you local environment and start on a new task

## Projects

See [Projects](./projects.md) for a list and summary of current projects being worked on by the tech committee, you may work on 1 or more of these projects at any time and switch between them at your preference

## Picking up Tasks in Let’s Go

Check the "To Be Started" tab for your committee to see tasks you can start working on

- The project name is usually included at the beginning of a task’s name
- Frontend and backend tasks have the FE and BE labels, respectively

How to assign yourself to a task and any guidelines associated with it, for example:

- You can freely assign yourself to any task under the “To be started” tab if the task has no other assignees. To see the list of assignees, click on the task card and navigate to the “Assignee” section under the task’s description.
- To assign yourself, click on the blue pencil next to the “Assignee” title and select your name from the list of members.
- If you see that the task of your interest is taken by someone else and if it’s a relatively new task, you can reach out to the member(s) assigned to it in Slack and ask if they would like to collaborate. Please do not assign yourself to the tasks that have other assignees without discussing it with the assignees first.

How to update the status of the task and any guidelines, for example:

- When a task is created by a team lead, its default state is “To be started”.
- Once a task is in progress (i.e., when the assigned developer starts working on it), the status should be changed to “In progress”.
- Once a task has been completed (i.e., the associated PR has been merged), the status should be changed to “Completed”.
- All members are responsible for maintaining the up-to-date status of their tasks.

## Setup your local dev Environment

Please see the initial setup guide [here](./edu/local-env-guides.md)

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

- [TailWindCSS](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)

  - Provides auto-complete and linting for css classnames

- [GitHub PR's](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)
  - Makes it very easy to work with PR's, provides the ability to submit reviews and suggestions from within VSCode

## Interacting with GitHub

### Cloning

Once you have access to a repo you can clone it locally and start coding. Cloning can be done with the `git clone` command or with Github desktop.

You'll need a `.env` file for the repos to run correctly, you can find these files on your EF Google drive. You can find them under `Shared Drives > Technology & Innovation > Technology & Innovation Shared Space > env`.

Once you download a `.env` file place it in the root of it's project and rename it to just `.env`

### Branching

Once you're ready to make some changes you'll need to create a branch first.

VSCode provides git integration automatically: you can click the
git branch button in the bottom left and choose `Create new branch`

The branch naming convention for both backend and frontend is `MMDD-<meaningful-name>`, where MM is the month and DD is the day of the branch was/is created

Once a branch is created you can safely commit to it, **never commit to main directly - always commit to your own branch**.

When you're ready to push your code to the remote repo, your command should look something like this:

```
git push origin 0623-add-widget-feature
```

### Making a PR

When you're finished with your ticket you can then open a Pull Request on github.

Opening the repo's github page in a browser after committing will show a button to quickly make a PR with your branch, you can also make a PR directly in VSCode if you have the extension installed.

Naming the PR the same name as the branch is acceptable if the branch name is meaningful enough.

You should also write a description for your PR and provide additional info (such as links to design pages or the TMA task link) to help reviewers understand your work / changes, if your PR depends on another PR or a backend change be sure to make note of this.

Take advantage of the many labels available on the GitHub repo to add descriptors such as `needs reviewer`, `not ready yet`, or `dependency` to provide quick information to reviewers.

Once you've posted your PR for review feel free to notify other devs on slack with a link to get some eyes on your work.

### Merging a PR

If your branch is out of date with `main` or if you have merge conflicts you'll need to pull the `main` branch into with yours and resolve conflicts.

Pay close attention when resolving conflicts as it's possible that you may overwrite or undo a teammates work.

You must receive 2 approvals from teammates to merge your PR to `main`.

You are not allowed to be a reviewer on a PR that you have worked on / committed to, exceptions can be made if your contributions are small or negligible.

Anyone on the team is allowed to merge a PR if the PR has 2 approvals.

When merging it is preferred that you use github's `squash and merge` function to keep the number of commits on the `main` branch low.

### Reviewing a PR

Please help us progress with the development by reviewing PRs of other team members.
Generally, we aim on getting at least two people to look over a PR and provide feedback and/or approval before merging it into `main` as a quality measure.

To review an open PR:

- Go to the GitHub repository and select the Pull Requests tab
- Select a PR that needs more reviewers
- Familiarize yourself with the task the PR is addressing, the task is usually linked in the PR description
- Check out the PR's branch and install and run the application
- Test if the PR meets the ticket's expectations, regarding both functionality and design
- Look into the code changes of the commits in the PR. Is it well implemented, understandable and good quality code? Here is a very detailed description of [things you might want to look at](https://google.github.io/eng-practices/review/reviewer/looking-for.html) for inspiration.

After your inspection, provide feedback in the PR by leaving comments. If you have found any bugs, inconsistencies, problems or concerns regarding the implementation or design, please describe your findings. The creator of the PR can then answer and/or make changes to the implementation.

When you are satisfied with the implementation, you can give your approval through a respective comment or GitHub's approval functionality.
