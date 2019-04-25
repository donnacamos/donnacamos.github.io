---
layout: post
title:      "OO Ruby Concepts, Part 1 : Object Behavior"
date:       2019-04-10 10:22:21 -0400
permalink:  oo_ruby_concepts_i_object_behavior
---



Ruby's object oriented programming is hard for me to get my head around. To help me understand OO Ruby better I've decided to write a mini-series solely focused on the concepts behind the programming.
 
I've found when learning anything, it's best to look up the definitions of the words themselves. What is Ruby programming and what's it used for? 
Let's ask Google:  

Ruby is a dynamic, interpreted, reflective, object-oriented, general-purpose programming language. It was designed and developed in the mid-1990s by Yukihiro "Matz" Matsumoto in Japan. According to the creator, Ruby was influenced by Perl, Smalltalk, Eiffel, Ada, and Lisp.

[Ruby (programming language) - Wikipedia](https://en.wikipedia.org/wiki/Ruby_(programming_language))

What can Ruby be used for?

It is used in a wide range of fields, but is best known as a language for Web Applications, because of the Ruby on Rails framework. The general purpose nature of Ruby makes it suitable for a wide array of programming tasks, just like Perl, Python and other general purpose languages.

[What is the Ruby language and in which field is it used? - Quora]
(https://www.quora.com/What-is-the-Ruby-language-and-in-which-field-is-it-used)

Great! Now that we know what Ruby is and what it is used for, we're ready to ask the next question. What is Object Oriented Programming? Google, if you please: 

Object-oriented programming (OOP) refers to a type of computer programming (software design) in which programmers define not only the data type of a data structure, but also the types of operations (functions) that can be applied to the data structure.

[What is Object-Oriented Programming? Webopedia Definition]
(https://www.webopedia.com/TERM/O/object_oriented_programming_OOP.html) 

You're probably thinking that I'm just looking up stuff on Google. And you'd be absolutely correct. Knowing how to use Google is one of the best skills a programmer can develop. It's a good idea to get really good at it by using it often. 

Now that we know what Ruby is, what it is used for and what object oriented programming, is we're ready to actually start coding. What I like to do is to get out a code block from Github, Codepen, or anywhere code is made and look at the code itself to break it down.Kind of like reverse engineering, only with code, you can use comments to explain as you go.
 
I'm not going to take the time to explain every concept of OO Ruby. Just the Object's behavior and how it can be used in programming. Let's get right into it with a block of code with an object `Cat` and make the `Cat` do stuff. Let's even give it a name. Then I'll start breaking down the concepts of the object's behavior. 

```ruby
class Cat # Cat is the object 
   def name=(cat_name) # the 'name' variable is created here 
       @this_cats_name = cat_name # Setter: sets up the variable for the object 
   end 
   def name # this is now an instance variable. It can be called to create new Cats. 
       @this_cats_name # Getter: gets the variable for the object 
   end 
   def meow # this is a local variable and can only be used make the Cat object meow. 
       puts "Meow!" # no new cats can meow here 
   end 
   def come # no new cats can come. Don't worry they won't come anyway. 
       puts "I'll come when I'm ready!" 
   end 
end 

garfield = cat.new
cat.name = "Garfield" 

puts garfield.name # "Garfield" Congrats! You've made a new cat! 

garfield.meow # Garfield can't meow. Why? meow isn't an instance variable like 'name'.
cat.meow # "Meow!" Cat can. Why? meow is a local variable. Only Cat can use it. 
``` 

This is a lot of code to begin with so let's build each method one at a time. 
First is the class method which acts as the blue print for building the object itself. 

```ruby 
class Cat 
# method body where stuff is built for the Cat 
end 
``` 
Now that we have the object Cat in our class method, let's write a local variable using an instance method and make the Cat meow. 

```ruby 
class Cat 
   def meow 
   puts "Meow!" 
   end 
end 

cat.meow # "Meow!" 
```
We made the Cat meow by creating an instance method within the class method. Instance methods make the object do stuff. The Cat can't meow unless the method is called using dot notation. Hence: 
```ruby 
cat.meow # puts "Meow!" 
``` 

This is great! Only now we need to name the cat. Since local variables can only work on the object Cat, we need to find a way to create new cats using all the same instance methods. Otherwise, we'd have to repeat all the instance methods for every new cat. Since we're lazy programmers it's better to just reuse all the methods in Cat for every new cat we want to create. How is this done? Enter the instance variable: 
```ruby
class Cat 
def name=(cat_name) # the 'name' variable is created here 
       @this_cats_name = cat_name # Setter: sets up the variable for the object 
   end 
   def name # this is now an instance variable. It can be called to create new Cats. 
       @this_cats_name # Getter: gets the variable for the object 
   end 
end 

garfield = cat.new
cat.name = "Garfield" 

puts garfield.name # "Garfield" Congrats! You've made a new cat!
``` 
Instance variables have two methods. The first method takes in an argument and sets that argument equal to a variable. The second method is responsible for reading or getting the name. The instance variable is called using the `@` symbol. This assures the attribute or in this case the `name` can be used to give other cats names, not just the object `Cat`. 
Instance variables are basically containers for attributes of the object, which is the topic of Object Oriented Ruby Concepts II. 
