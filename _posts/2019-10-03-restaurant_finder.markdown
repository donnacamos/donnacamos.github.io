---
layout: post
title:      "Restaurant Finder"
date:       2019-10-04 01:27:14 +0000
permalink:  restaurant_finder
---

## Rails Portfolio Project

Rails was tough to get through! Mostly because I kept forgetting how to do simple things like adding in my routes. Everything seemed really spread out and out of order compared to Sinatra. But after going through the lessons and videos again and building an almost completed project, I was finally able to put the pieces together in my head. All in all, Rails is faster and way more streamlined than Sinatra and I can see the advantages to using it as opposed to Sinatra. 

First, I needed to look over the requirements and plan the project. I didn't want to do a blog (wasn't allowed to by Flatiron anyways) since my last project was a blog, so I decided to put out a vote on Twitter. The "Restaurant Finder" won by a small margin and I set out to build a mock "Yelp" app. 

The app was to have models that interacted with each other with a parent-child relationship of has_many and belongs_to. I wanted to go with the recommended amount of four separate models. It took me half a project before I realized my models of User, Restaurant, Review and City weren't going to work. I needed to change City to something that would relate to Restaurant better. So I chose Company. It took me another half a project later on my second attempt to realize this wouldn't work either. Finally, I came to my senses and chose Category, letting the user choose what kind of restaurant they were cataloging and reviewing. 

 I started with the Rails generators. I wasn't allowed to use Scaffold and to be honest, I didn't really want to. I had enough code to keep track without having to worry about extra code lying around. I went with Resource, which is my personal choice for Rails generators. It gives you your migration file, model file, controller file and view folder as well as setting up the routes. 
 
 
 After setting up my models, I started to build out the associations of has_many, belongs_to, and has_many, through. After that, I was able to start with building out my controllers to get a welcome page set up in the views/sessions file. I also added a sessions controller file to control the users logins, whether by password or with a third party login service. I chose Google for this, which you can find instructions for [here](https://medium.com/@amoschoo/google-oauth-for-ruby-on-rails-129ce7196f35). 
 
 After setting up my Sign up and Login pages, I started building out my restaurants/new file in my views. This is where it got tricky. I needed a form that would let me put the restaurant information in it, which required logic in my controllers and the correct path in my routes. It took me a very long time to put this part together compared to setting up the app with the login and sign up. But after looking through several Flatiron example projects and watching this [video series](https://instruction.learn.co/student/video_lectures#/455) by Jenn Hansen at Flatiron School, I set up the restaurant/new page for the user's restaurant information.
 
 This app also had a restaurant index page, a create a review page, an index review page and a categories index page. The app is very simple and straightforward. I kept it that way on purpose to stay within the requirements and to help me understand the nature of Rails before embarking on a more adventurous project. I learned a lot from building it out and I'm excited that I feel competent that I understand how it works "under the hood." 
 
 Resources: 
 
 * [Restaurant Finder](https://github.com/donnacamos/restaurant-finder)
 
 * [Ruby Style Guide](https://github.com/rubocop-hq/ruby-style-guide)
 
 * [Rails Style Guide](https://github.com/rubocop-hq/rails-style-guide) 
