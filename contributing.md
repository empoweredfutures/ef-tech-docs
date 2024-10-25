# Contributing

The current projects under development are:

EF Connect
“EF Connect” (internally known as "Mentorship Platform (MP)") is Empowered Futures’ core product. It is an online platform connecting young people seeking guidance (i.e., mentees) with experienced professionals (i.e., mentors) ready to mentor and support their growth. It allows mentees to create a profile, search for and send mentorship requests to mentors who are registered in the mentorship platform, and schedule meetings based on the mentors’ availability.
Slack channel: #mentorship-platform
GitHub link: https://github.com/empoweredfutures/mentorship-platform
App: https://calm-moss-0b0b59d10.5.azurestaticapps.net/ ( still in development )
You can check out the mentorship-platform readme for more information about the intent, flow, and features of the project.
EF Website

“EF Website” or just “Website”
Slack channel: #website-dev
GitHub link: https://github.com/empoweredfutures/EF_Website
Deployed app: 

Let’s Go
“Let’s Go” (internally known as “Task Management App (TMA)” or “Internal FE”) is our internal project management tool. Designed to maximize efficiency, our app streamlines task assignments and accountability, helping us create, build, and support the Empowered Futures brand in fulfilling its mission.
Slack channel: #internal-project
GitHub link: https://github.com/empoweredfutures/internalFE
Deployed app: https://go.empoweredfutures.ca/

Android and iOS exports of EF Connect
Slack channel: #native-mobile-dev
GitHub link for the Android app: https://github.com/empoweredfutures/mentorship-platform-android
GitHub link for the iOS app: https://github.com/empoweredfutures/mentorship-platform-ios
App: Is still in development


To contribute to the projects in Empowered Futures, check out [Lets Go](https://wonderful-tree-0ee814e0f.5.azurestaticapps.net).

Once you've joined the "Tech" committee you can visit the committee tasks from the side menu. You'll see list of tasks that you can work on in the "Incomplete" section.

When you've decided on a task you want to start you can add yourself as a assignee on the task, then mark the task as "In Progress".

That's it - you can make a branch (see below) and get started!

Before you start coding, below are some key pre-requisites we all have to comply with.

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

## Setup your local dev Environment

See the full setup guide [here](./edu/local-env-guides.md)

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
