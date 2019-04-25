---
layout: post
title:      "OO Ruby Concepts Part 2, Object Attributes "
date:       2019-04-11 18:24:24 -0400
permalink:  oo_ruby_concepts_ii_object_attributes
---


Last [post](https://dev.to/donnacamos88/oo-ruby-concepts-i-object-behavior-308a) I discussed objects and their behavior. This post will cover the attributes of an object and how to manipulate them to cause a certain behavior. 
   Every object has attributes. To make this clear, I looked up the definition of "Attribute" on Google and here's what it said: 

at·trib·ute

verb
1.
regard something as being caused by (someone or something).
"he attributed the firm's success to the efforts of the managing director"

noun
1.
a quality or feature regarded as a characteristic or inherent part of someone or something.
"flexibility and mobility are the key attributes of our army" 

Let's stick with our Cat class from the previous post and give it two attributes, name and breed, using the 'setter' and 'getter' instance variable methods. 
```ruby
class Cat # Object 
  def name=(garfield) #setter 
  @name = garfield 
  end 
  def name #getter 
      @name 
  end 
  def breed=(tabby) #setter 
     @breed = tabby 
  end 
  def breed #getter 
     @breed 
  end 
 end 
 
garfield = Cat.new("Garfield") 
garfield.name # "Garfield" 
```
This block of code contains both a "setter" and "getter" method which writes or sets the attribute and then reads or gets the attribute for the object to use. This code is long and becomes repetitive very quickly and unless you need to customize it, there's a better way to set and get attributes. 
 We use macro programming to accomplish this. Macros are a tool that allow programmers to reuse code. Attribute readers and writers are macros that implement this same code above with only two lines of code. 
```ruby 
class Cat 
   attr_writer :name, :breed  #setter
   attr_reader :name, :breed  #getter 
end 
```
As you can see, much more efficient. William Strunk, in his classic book "The Elements of Style" said, **"Omit needless words"**. Macros in programming **omit needless code** and allow the attributes to be added much more seamlessly. The attribute writer and reader can be further condensed with the attribute accessor like this: 
```ruby 
class Cat 
    attr_accessor :name, :breed # setter and getter all in one line
end 
```
Now let's make a new cat, with a name and breed and make it "Meow!" using the attribute accessor.  
```ruby 
class Cat 
    attr_accessor :name, :breed 
    def meow 
    puts "Meow!" 
    end 
end 

garfield = Cat.new 
Cat.name = "Garfield" 
garfield.name # Garfield 
garfield.breed = "Tabby" 
garfield.breed # Tabby 
garfield.meow # Meow! 
