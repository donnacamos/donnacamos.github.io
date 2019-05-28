---
layout: post
title:      "My First Ruby CLI Data Gem "
date:       2019-05-23 17:39:39 -0400
permalink:  my_first_ruby_cli_data_gem
---

Building a CLI Gem in Ruby was the hardest thing I've ever had to code. I tried following the instructions from several videos (watching them all twice just to make sure I could understand them), took notes and studied the github repositories of other's cli gems.

But I wasn't getting anywhere after several weeks. I tried to set up another repository after my first attempt failed. Usually with projects I find it helps to have more than one version. The first is my practice run, the second is usually my finished product. But this failed miserably. 

I tried going back to basics and just kept it simple. Just remember you build methods, connect them and call them. If you can remember when to connect them and when to call them it will save you time, effort and a headache. It might even be fun! 

If I had to do this over again, here are the steps I would use to be more systematic in my approach: 
### 1. Set Up the Gem 
The CLI Gem I created is called 'Makeup-Sales-CLI-Gem.' It lets you see the sales going on at Ulta Beauty's website. First, set up a new Github repository. Watch this [video](https://www.youtube.com/watch?time_continue=317&v=YZNXWWHUO-E) to help you set up your project in the IDE.
Now that the Github repository is set up you need to make sure your folders and files are set up. 
I named the gem 'Makeup-Sales-CLI-Gem'. Within that gem I had three folders: bin, config, and makeup-sales. 
Setting up the gem should be straightforward but unless you put the right gems (e.g. nokogiri) in the right files, you'll continue to run into errors. 

The makeup.gemspec file should have these dependecies with the updated versions:
 
  spec.add_development_dependency "bundler", "~> 2.0"
  spec.add_development_dependency "rake", "~> 10.0"
  spec.add_development_dependency "rspec"
  spec.add_development_dependency "pry"

  spec.add_dependency "nokogiri"
	
Now you should be ready to modify your README file which tells the user what the gem is all about and how to use it. 
### 2. Set up the README  file
Give a short description on what your gem does when it's run and installation instructions for the user to follow to run the gem.  Like this: 

# Makeup Sales

Welcome to the Makeup Sales CLI Gem! 

Follow the installation instructions below to see the sales going on at Ulta Beauty's website.  

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'makeup-sales-cli-gem'
```
Install nokogiri 

```ruby
gem install nokogiri
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install makeup-sales-cli-gem 

## Usage

Type the below and follow the screen prompts

    $ ./bin/makeup-sales

Requiring nokogiri and installing it are two different things. I found this out the hard way. I had required nokogiri but didn't know I was also supposed to install it in the IDE until I read about it in another blog post. It's the little things that matter most when it comes to coding so be sure to pay attention and don't be afraid to go looking for answers on your own and ask for help if the CLI isn't running correctly after several attempts and you don't understand the errors.  
To install nokogiri type this in the command line:
```ruby 
gem install nokogiri
```
Now I'll move on to set up the Bin and Config Folders
### 4. Set up the Bin Folder and  the Config Folder  
The great thing about Ruby programming is everything is connected to everything else. It's like playing dot to dot. I need to create a makeup-sales file in the bin folder to run the gem.
```ruby 

#!/usr/bin/env ruby # the shebang line tells the program loader what command to use to execute the file 


require_relative '../lib/makeup-sales'  # calling the makeup-sales file 

MakeupSales::CLI.new.call # callling the cli, new method creates a new call class method allowing the gem to run it's                                                             #  methods and allowing the user to see the gem running on the command line 

```
The config folder contains the environment.rb file which takes the links of all the files and puts them in one place to keep them all connected. 
```ruby 
require 'nokogiri'
require 'open-uri'
require 'pry' 

require_relative '../lib/makeup-sales/scraper'
require_relative '../lib/makeup-sales/product'
require_relative '../lib/makeup-sales/cli'
require_relative '../lib/makeup-sales/version'
```
### 5. Set up the Lib folder 
The Lib folder is where I'll build the gems methods to get it running. I'll need a makeup-sales.rb file to hold the module 'Makeup-sales'. 
```ruby 
module MakeupSales  # connects the files in the MakeupSales folder 
end 

require_relative '../config/environment' # compiles the files together with the dependencies allowing the gem to                                                                                              # function
```
### 6. Makeup-Sales file - CLI, Product, Scraper, Version 
Time to create the gem itself. All the code for this gem to run will go in a folder called 'Makeup-Sales' which consists of four files: CLI.rb, Product.rb, Scraper.rb, Version.rb. The .rb is added to tell the IDE you're writing in Ruby. 
CLI.rb file:
```ruby 
class MakeupSales::CLI    #MakeupSales is the module, CLI is the class 

  def call
    MakeupSales::Scraper.scrape_product  # Calling the Scraper method  
    puts "\nWelcome to the Makeup Sales of Ulta Beauty:\n" # This is what the User sees
    main_menu  # calling the main_menu method
  end
  
  def main_menu # this gives the user the option to view the products 
    puts "Type 'list' to see a list of the products."  
    puts "Or type 'quit' to leave." 
    input = gets.strip.downcase  # this method allows the user  to choose what input they want
    case(input)  # this case statement has the argument of input; the outcome is determined by the user's input
    when 'list' 
      product_list # product_list is called from below when the user types 'list'
    when 'quit'  
      goodbye  # calls the goodbye method 
    else
      puts "Invalid Entry"  # anything the user types other than 'list' or 'quit' 
      main_menu # loops back to the beginning 
    end
  end
  
  def product_list   
    puts "Here are the beauty products on sale today:\n"
    MakeupSales::Product.all.each.with_index(1) do |product, idx| # shows the products in list form each with index
      puts "-------------------------------------------------"                     # MakeupSales::Product.all calls the products you've
      puts "#{idx}. #{product.brand}"                                                      #  pushed into the @@all array from the Product class 
      puts "#{product.description}"                                                        # this method uses interpolation to call the scraped data
      puts "Sale Price:#{product.sale_price}"                                     # from the MakeupSales::Scraper class
      puts "Original Price:#{product.previous_price}"
      puts "-------------------------------------------------"
     end
      puts "\nSelect a number for the product you want more info about."
      input = gets.strip.to_i - 1  #index value 0-98     
      max_input = MakeupSales::Product.all.size - 1 # max_input puts a stop on how many numbers the user can correctly       until input.between?(0,max_input)                         # input, in this case 1 - 98 is allowed
       puts "Sorry, please enter a number between 1 and #{max_input + 1}"
       input = gets.strip.to_i - 1 
     end
     
      product_object = MakeupSales::Product.all[input] # creating a variable from Product class and calling @@all array
      MakeupSales::Scraper.scrape_product_details(product_object)  # calling Scraper class
      puts product_object.more_info  # calling this method from Scraper class
      next_product  # giving the user the option to return to the main menu 
  end 
  
  def next_product 
    puts "\nWould you like to see another product? Y or N?"
    answer = gets.strip.downcase 
    if answer == 'y' 
      puts product_list  
    elsif answer == 'n' 
      puts goodbye 
    else 
      puts "invalid entry" 
      next_product 
    end 
  end 
  
  def goodbye 
    puts "Thank you for shopping with us! See you soon!" 
  end
 
end  
```
Product.rb: 

```ruby 
class MakeupSales::Product
  
  attr_accessor  :brand, :sale_price, :previous_price, :description, :url, :more_info   
  
  @@all = []  # all products are in this array
  
  def initialize(brand)
    @brand = brand  
     @@all << self # pushing the products into the @@all array 
     
  end 
  
  def self.all 
    @@all 
  end 
  
  
end 
```

Scraper.rb file:

```ruby 
class MakeupSales::Scraper 
  
  def self.scrape_product 
    
    website = Nokogiri::HTML(open("https://www.ulta.com/promotion/sale")) #Scaping from this url
     section = website.css("ul#foo16") # the unordered list which contains the products
     products = section.css("li") # products are contained in the list item or 'li' HTML tags 
    
   products.css("div.productQvContainer").each do |product|  # iterate over the products in this div container with each
      brand = product.css("h4.prod-title").text.strip # created the brand variable to initialize in the Product class
      product_object = MakeupSales::Product.new(brand) # create the product_object instance variable
      product_object.description = product.css("p.prod-desc").text.strip # scrape the product_object's attributes
      product_object.sale_price = product.css("span.pro-new-price").text.strip
      product_object.previous_price = product.css("span.pro-old-price").text.strip
      product_object.url = "https://www.ulta.com" + product.css("a").attr("href").value # url is a combination of the original                                                                            # url plus the scraped data of each individual url tags contained in the anchor tags
    end 
  end 
  
  def self.scrape_product_details(product_object) # this method gives each individual product a seperate description 
    website = Nokogiri::HTML(open(product_object.url) # because of the product_object.url variable
    product_object.more_info = website.css(".collapse.in").text.strip
  end 
   
end 
```

Version.rb file:

```ruby 

module MakeupSales

    VERSION = "0.1.0"
		
end
```


### 7. Ask for Help If You Get Stuck
This project took me over a month and I had to go over each basic concept no less than three times and watched the videos twice. It looks simple but keeping it simple is the real challenge. I couldn't have done it without the help of several teachers from Flatiron School. 

Sometimes the answer is simple if you know what to look for but if you don't it can take you longer than it should. I regret that I didn't ask for help sooner or more often but I don't regret the amount of study and work I put into it. 
Don't be afraid to review. If you feel like you're over reviewing, you're probably doing it right. Don't get discouraged. Coding is complicated and isn't meant to be picked up overnight. If you're frustrated take a break. Go over everything slowly and be sure to take care of yourself. 

I hope this helps you in building your CLI Gem. I learn best from documented code explaining what every method's purpose is and what it's doing. Here's the Github [link](https://github.com/donnacamos/makeup-sales-cli-gem) if you want a better idea of what the structure is for a Ruby gem. 

Good luck and happy coding! 


