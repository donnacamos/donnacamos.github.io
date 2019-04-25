---
layout: post
title:      "OO Ruby Concepts Part 3, Object Relationships "
date:       2019-04-25 02:30:50 +0000
permalink:  oo_ruby_concepts_part_3_object_relationships
---


![alt text](https://vignette.wikia.nocookie.net/playstationallstarsfanfictionroyale/images/9/90/BF7_garfieldoddie.jpg/revision/latest/scale-to-width-down/200?cb=20130425191848)

Last [post](https://dev.to/donnacamos88/oo-ruby-concepts-ii-object-attributes-5708) we gave an object its attributes so it can become its own entity. But the object we made, Garfield, can't interact with any other objects. That's where object relationships comes in. If objects are modeling real world entities, they need to have a method to know who they belong to. This method is called "belongs to". Let's start with building the "Garfield" object. 

```ruby

class Cat #object 
     attr_accessor :name # gives the object a name
  
   def initialize(name) # Initialize method means the name attribute is called when #new is called 
     @name = name 
   end 
end 

garfield = Cat.new("Garfield") 


``` 
Now that we have made a cat object, Garfield, we need to give him an owner. Who else will feed him lasagna? 

 
```ruby 

class Owner #object 
     attr_accessor :name, :job # attributes about the object 

  def initialize(name, job) # Initialize method means the name and job attributes
    @name = name            # are called when #new is called.  
    @job = job 
  end 
end 

 jon = Owner.new("Jon", "cartoonist") # new method names the Owner, Jon, 
                                      # and gives him a job, cartoonist  

 garfield.owner = jon # Congrats! Now Garfield belongs to Jon. 

```
Now Garfield knows that he belongs to Jon. However, what if Jon wanted another pet? In the real world, he can own as many pets as he wants. He's decided to get a dog. How do we give Jon another pet? 

With a method is called the "has many" relationship. It allows an object to have many objects and relate to one another. In this example, it allows the Owner, Jon, to have two pets. And any more if he wants them.  

```ruby 

Class Owner 
   attr_accessor :name, :job 

 def initialize(name, job) 
   @name = name 
   @job = job 
   @pets = [] # this empty array is where all Jon's pets will go 
 end 

 def add_pet(pet) # this method allows Jon to add as many pets as he wants
   @pets << pet # the shovels(<<) push the pet class we've created into the array
 end 

 def pets # this method simply returns the @pets array when it is called
   @pets 
 end 
end 

 jon.pets # => ["Garfield", "Odie"] this is the pets array when it is called
  

```

Now we need to make an Object called Pet that we can use to give Jon more pets when this method is called. 

```ruby 

class Pet 
       attr_accessor :name, :species  

   def initialize(name, species)
    @name = name 
    @species = species 
   end 
end 

  odie = Pet.new("Odie", "dog") # "Odie" is the name, "dog" is the species
  garfield = Pet.new("Garfield", "cat") # Congrats! Jon can now adopt his two pets.

```
One more method to bring all this together. The self keyword refers to the owner we're calling on.  


```ruby 

   pet.owner = self 
 

```
Add this to the `add_pet` method so we can call the `self` keyword to let the pet know who his owner is.  

```ruby 

Class Owner 
   attr_accessor :name, :job 

 def initialize(name, job) 
   @name = name 
   @job = job 
   @pets = [] 
 end 

 def add_pet(pet) 
   @pets << pet 
   pet.owner = self # self keyword 
 end 

 def pets 
   @pets 
 end 
end 


 jon.add_pet(garfield) # calling the add_pet method 
 
 garfield.owner.name # => "Jon", Garfield knows Jon is his owner 

 jon.add_pet(odie) 

 odie.owner.name # => "Jon", Odie knows Jon is his owner 

 # Now Jon has two pets and they know they belong to him!

```
