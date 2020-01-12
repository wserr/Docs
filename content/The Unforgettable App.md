---
title: "The Unforgettable App"
metaTitle: "The Unforgettable App"
metaDescription: "Build something you won't forget with ASP .NET (core)"
---

# Build something you won't forget with ASP .NET (core)

#### Watch the catch phrase that almost rhymes

I recently moved to a new place with my girlfriend. Being away from home for the first time means a lot of new challenges, the biggest one for me having a tendency to forget a lot of important chores like paying the rent, watering the plants, ...

The next problem is getting groceries. My girlfriend and I often need to go to the supermarket twice or more a week, because we forgot something the first time. It happens a lot, when we start cooking, we notice that some ingredient is missing, and we have to revisit the store. Or eat something that doesn't quite taste as it should...

To solve these problems, I decided to build an app that will help my girlfriend and I keep track of all the things we need to remember.
In this series of articles, I will describe the different parts of the app, without going into great detail. You can find the source code [here](www.google.com).

## Goals of this project

I will divide the goals into 2 parts
- Functionality: the things I want to be able to do with the app
- Technical: the various parts of .NET core that I want to have a better understanding of at the end of the development

### Functional goals

- Create reminders for every month, year, week, ...
- An overview that shows al reminders for current day
- Create meals and add ingredients to them
- Week overview that lets the user the ability to assign one or more meals to each day
- Let users have the possibility to log in
- Users cannot register themselves. The administrator needs to add the users to the database

### Technical goals

- Unit test every functionality with NUnit
- Use AspNetCore.Identity to keep track of users
