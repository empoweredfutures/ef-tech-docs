# Mentorship Platform

This document details the scope and functionality for the Mentorship Platform project as it pertains to reaching MVP status

---

## Intent

This platform is meant to be used by two types of users, Mentors and Mentees.

A Mentor will be able to get mentoring requests from Mentees, set their availability, and have meetings booked around their provided schedule.

A Mentee will be able to search for mentors by a set of filters, send a Mentor a request with a summary of why they want a mentorship, and then, if they are accepted by the Mentor, book a meeting with the Mentor.

## Flow

### Mentor

For a user to become a mentor the following flow must occur:

- select `become a mentor` on the EF MP homepage
- enter an email and verify it
- fill out the detailed application form with relevant information
- get approved by an EF Admin internally to verify their status as a mentor
- use the `magic link` delivered to the user's email upon being approved by an admin to login / set a password
- setup their profile and availability

### Mentee

For a user to become a Mentee all that is required is that they signup with either a valid email or using Google OAuth.

## Features

**All** users should be able to perform these actions:

- login / signup / logout
- edit their personal info / profile, including their picture
- edit additional settings relating to their account and email
  - eg: notification preferences, email subscriptions etc...
- attend meetings
  - just a link to google meets
- delete their account

All **Mentors** should be able to perform:

- setting their availability
- accepting / rejecting mentees
- viewing their calendar

All **Mentees** should be able to perform:

- searching for mentors
  - with relevant filters
- sending requests to Mentors with their summary
- see their upcoming meetings

## Technical Information

The mentorship platform uses the following technologies:

Backend:

- NodeJS, ExpressJS, PassportJS, PostgreSQL, Prisma, Zod, NodeMailer, googleapis, jsonwebtokens, bcrypt, azure-blob-storage

Frontend:

- ReactJS, NextJS, TailWindCSS, date-fns, Axios
