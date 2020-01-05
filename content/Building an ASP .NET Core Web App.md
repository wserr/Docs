---
title: "Building an ASP .NET Core Web App"
metaTitle: "ASP .NET Core Web App"
metaDescription: "This section describes how I built my ASP .NET Core Web App"
---

# Introduction

I recently moved to a new place. Away from living with my mother, this proves to be quite a challenge. The biggest problem I have is that I tend to forget a lot of stuff: doing the dishes, getting groceries, pay the rent, ... 

The next problem is the groceries part: my girlfriend and I often need to shop for groceries twice or more in a week, because we forgot something the first time.

To help solving these problems, I decided to build an app that will help me and my girlfriend keep track of all the things that I need to remember.
In this series of articles, I will describe the different parts of the app, but I will not go into great detail. Checking out the source code is possible on Github (TODO WIS add link to github page)

## Goals of this project

I will divide the goals into 2 parts
- Functionality: the things I want to be able to do with the app
- Technical: the various parts of .NET core that I want to have a better understanding of at the end of the development

### Functional goals

- [ ] Create reminders for every month, year, week, ...
- [ ] An overview that shows al reminders for current day
- [ ] Create meals and add ingredients to them
- [ ] Week overview that lets the user the ability to assign one or more meals to each day
- [ ] Let users have the possibility to log in
- [ ] Users cannot register themselves. The administrator needs to add the users to the database

### Technical goals

- [ ] Unit test every functionality with NUnit
- [ ] Use AspNetCore.Identity to keep track of users
