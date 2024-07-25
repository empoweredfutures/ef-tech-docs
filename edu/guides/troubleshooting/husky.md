## Husky Troubleshooting

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
