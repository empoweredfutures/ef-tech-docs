# Switching Accounts

### Create the accounts

first you'll have to create the 2 accounts that you'll switch between, one of these accounts should be a real account made with google oauth

once you have your real account you can make the second account manually or with the seed mutations

### Switching

once a second account has been made open prisma studio (`npm run studio`)

open the `User` collection and scroll until you see the `Account` and `Session` relations in the table header

your real account will likely be the first row in the table and it should be the only row that has a `1` for the `Account` and `Session`

find the other account in the row that you want to switch to

click on this other `User`'s `Account`, you will get a window that list accounts the you can select

select what should be the only row in the `Account` table (your real accounts row) and check the box, once it's selected save your changes

you must now do the same process but with the `Session`

once both `Account` and `Session` are switched to the second account you can refresh the web app in the browser and you'll be signed in as the other user

you can switch the `Account` and `Session` to any other user or back to your personal account whenever you'd like through prisma studio
