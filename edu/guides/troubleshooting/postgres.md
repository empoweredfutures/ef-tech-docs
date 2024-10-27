# Postgres Troubleshooting

it is recommended that you [reset your database](/edu/local-env-guides.md#resetting-your-database) every time you develop to ensure that you always have a clean db that is synced with the latest changes to the schema

if your issue is that you cannot connect / push to the database try changing your `.env` files `DATABASE_URL` variable, change the `user` in the url to your username on your machine, this has been found to be the case on certain MacOS machines
