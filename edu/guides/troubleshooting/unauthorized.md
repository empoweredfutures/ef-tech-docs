## 401 Unauthorized Troubleshooting

in almost all cases this is caused by not having a valid auth session in the application

most commonly happens when `/api/gql` is visited before logging into the application on the homepage

it can also happen when you've reset your database and your previous session is no longer valid

in all cases it can be fixed by visiting the homepage and signing in with your google account
