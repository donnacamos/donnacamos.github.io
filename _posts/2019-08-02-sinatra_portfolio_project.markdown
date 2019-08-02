---
layout: post
title:      "Sinatra Portfolio Project"
date:       2019-08-02 21:19:32 +0000
permalink:  sinatra_portfolio_project
---

## Baker's Blog App 

Building a Sinatra Project was a little easier for me than the initial CLI Data project, mainly because I was familiar with the basic Ruby concepts of object-oriented programming and also their was a [video series](https://instruction.learn.co/student/video_lectures#/353) on Learn Instruct about how to build out a project with Sinatra by Howard Devennish. I'd probably still be wandering around Google if it wasn't for that series. 

Thankfully, Flatiron provided a lot of practice for me with their labs in building out a Sinatra project. The things that I had to conquer the most were understanding the MVC models and RESTful routes. Once I understood that the models were holding the data using the ActiveRecord gem, the controllers were using RESTful routes to control the actions of the data that the user had called and the views were allowing the user to see the pages that were called with the specified data, I was able to understand the process of how everything was functioning in Sinatra. 

Baker's Blog is a simple blog app used for recording baking experiences and recipes.

User's experiences: 

* Create an account using their name, email and a password (encrypted)
* Login if they have an existing account
* Create a new post
* View a previous post
* View other's posts
* Edit their own posts 
* Delete their own posts 
* Logout 

As the developer, I needed to build: 

* Models 
* Associations for those models 
* Data contained in the models 
* Schema file to contain the migrated data
* Separate controller routes for each model 
* Helper methods for the routes contained in the application controller file 
* Views folders for the user to Create, Read, Update and Destroy their account's content 
* Mount the controllers in the config.ru file 

This process took me longer than I expected for this particular project, since I scaled it down so much but it was so much easier than my first project because I worked very hard to understand the concepts of Sinatra and I feel I have a good handle on the concepts of Object Oriented Ruby.

The biggest piece of advice I can give is ask early and ask often. And take lots of notes while watching the videos. Also, I went very slow through the process until I understood what each method's purpose was and what it was doing. 

* Video and GitHub Repository Links: 

[Video Demo](https://www.youtube.com/watch?v=hwml74THVwQ)

[Baker's Blog App](https://github.com/donnacamos/bakers-blog-app)
[Example Project](https://github.com/learn-co-curriculum/example-sinatra-assessment)
[Howard's Journal App](https://github.com/howardbdev/sinatra-journal-app)

 







