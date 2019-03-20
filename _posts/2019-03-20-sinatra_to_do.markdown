---
layout: post
title:      "Sinatra To Do"
date:       2019-03-20 18:25:56 +0000
permalink:  sinatra_to_do
---


My Sinatra To Do List is a simple application, using **MVC** and **Active Record**. At the time of this posting, the application has two models, user and task. Users must log in to view their To Do List, and may only see their list. The user is able to then perform **CRUD** actions on task objects. Upon login, the user is redirected to their show page. The show page lists their name, email address and tasks.

The **bcrypt** gem was used to secure users' passwords. Rails method '**validates_uniqueness_of**' was used to prevent duplicate usernames and email addresses. 

Building this application has reinforced the need for me to check my routes as I build them. Checking as you go makes troubleshooting much easier. Working through this project has deepened my understanding of Ruby and Sinatra.

[Github Sinatra To Do](https://github.com/Connieh1/to-do-sinatra.git)
