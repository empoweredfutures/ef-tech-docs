# Tech Ops

this document outlines basic instructions for being a tech-ops team member

## Responsibilities

a tech-ops members' main task is to add new members to the organization, though occasionally you'll need to provide other assistance, such as resetting password, troubleshooting, and misc account management jobs that only a google admin can do

### Adding a User

this section outlines how to add users to the org using the `ef-user-req-tool` and the google admin dashboard

#### Start

- first visit https://ef-user-req-tool.up.railway.app and log in
  - _you will only be granted access to the web app if you are using your EF google account!_
- once signed in the main page will display a list of recent user requests, the requests that are completed have a green background
- select (click) a request that has not yet been completed, you'll be taken to the `view` page
- once the `view` page is open, open the google admin dashboard (https://admin.google.com) in a new tab
- once you re-enter your password on G Admin you'll arrive at the dashboard
- you'll see a block on the interface for `Users`, within this block you'll see `add a user`, select that option
- you'll get a "pop-up style" page asking for information about the user you want to add

#### Filling in the user

- fill in this information with the info provided on the `ef-user-req-tool` in your other tab
  - the "Primary Email" is the user's EF Email, the "Secondary Email" is the user's personal email
  - _**additionally take a moment to ensure that the EF Email matches the pattern that we use for all EF members**_
  - this pattern is as follows: the first letter of the user's first name (or the first letter of their preferred name) and the user's full last name (or preferred last name)
  - so a user such as "`John Doe`" would have an EF email of "`jdoe`"
  - the `ef-user-req-tool` should generate this for you but it's a good idea to verify it yourself
  - the `ef-user-req-tool` is **NOT** aware of edge cases such as already taken EF addresses
  - if you do run into a situation where the email is already taken the solution is to add 1 additional letter to the first name, so "`John Doe`" would be "`jodoe`" if "`jdoe`" was already taken
  - you should also update the request on the `ef-user-req-tool` itself when it gets the EF Email wrong
- once you've filled it all out the user's information click "add new user"
- the following page will have 2 buttons you need to click, one to copy the password and one to send the user an activation email, _you must do both_

#### Sending a Welcome Email

- once you've done those 2 actions, open your EF Gmail in a new tab, choose compose to start a new email
  - switch back to the `ef-user-req-tool` and you'll find a "`copy welcome email`" button at the bottom of the page
  - click this and paste it into the new email you are composing in your other tab
  - make sure to proof-read the welcome email to ensure the `ef-user-req-tool` filled in all the user's personal info
  - you'll also notice that developers (tech team members) have a text block at the bottom of the email, **Remember to remove this text block for non-tech members**, if the user is a tech member then remove the `IF DEVELOPER` and `END IF` lines
- cut and paste the `TO:` address into the `To` address bar, and cut and paste the `SUBJECT:` text into the `Subject` bar, removing the place holders afterwards
- paste the password you copied when you made the user in place of the `PASSWORD` text
- if everything looks good then send it to the user

#### About Google Groups

- when you create a user in g admin you must also add them to corresponding groups
- every user must be added to the "members" group for all members
- after that the user must then be added to their specific committee group
- in many case you must just add the user to the closest matching group name
  - for example "Mobile Developer" gets added to "technology" and "mobiledev", while "Talent Acquisition Specialist" just gets added to "talentacq" alone
  - another example: a "Tech (Frontend)" and a "Tech (Backend)" both just get added to the "technology" group, but not "mobiledev"
  - you'll have to use your best judgement to assign users to their groups
  - if you are confident that a group / committee does not exist then you'll need to create the group much in the same way that you create a user

#### Adding Members to Groups

- lookup the user you just created by pasting their EF or personal email into the large search bar at the top of g admin
- once found, select the user, you'll be taken to their user page
- on this page scroll down to groups and assign the user to the appropriate groups, remember that all users must get added to the "members" group

#### Completing the Request

- once all this is done you can return to the `ef-user-req-tool` and change the "`Status`" of the request to complete using the `Edit` and `Save` buttons
