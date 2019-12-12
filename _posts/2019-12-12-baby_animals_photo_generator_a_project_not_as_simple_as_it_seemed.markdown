---
layout: post
title:      "Baby Animals Photo Generator: A Project Not As Simple As It Seemed"
date:       2019-12-12 17:53:14 -0500
permalink:  baby_animals_photo_generator_a_project_not_as_simple_as_it_seemed
---

## JavaScript/Rails Project for Flatiron School 

The biggest mistake I made going into this project was thinking I understood the basics of object oriented JavaScript because I understood the basics of object oriented Ruby. JavaScript it seems, is it's own unique kind of programming language where it plays more the role of the middle man for the programming process in that it tells the HTML what to display and when and fetches and processes the data it receives from the API. 

This project probably would have gone faster if I had slowed down a bit and reread some of the material a little more. I didn't shirk on asking for help and watching the practice videos. Since the videos I watched were very simple and more streamlined than what I was trying to build, I had a hard time translating that into what I was trying to build once I got to JavaScript section of the project. 

I came up with this idea while on Twitter. When people were having a bad day, they would ask their friends and followers to tweet animal pictures to help them feel better. So, I thought why not make an app specifically for what they were asking for to help them on a bad day? After all, not everyone wants to tell the whole of Twitter when they're having a hard time, so they can still relax and enjoy cute animal pics if it makes them uncomfortable to talk about it. 

### Building The Rails API 

Building out the Rails API was definitely the shortest part of this whole process. I've done a project with Rails before and understood most of the process already. The only snag I really hit was running the Rails server with `rails s`. The server would fail to run in my terminal and I kept getting these weird errors. I Googled the problem and found a solution on Stackoverflow.com, `rails s -p 3001`. Now the server ran but not on the default port 3000 but on the specified port of 3001.  

### Fetching The Data From the Database 

Fetching the data from the database was incredibly confusing to me. I got so lost, I had to schedule a meeting with Howard, a Flatiron School instructor. He stayed with me for an hour and a half explaining the process from database to browser and helping me to understand line by line what the JavaScript code was that I needed to get the photo urls from the database to show on the browser. 

Here's the code he helped me come up with, 
```
// array where all the photos are stored 
let allPhotos = []; 
// wait for the DOM to load 
document.addEventListener("DOMContentLoaded", init);
  
function init(){
    // these are the things that need to happen when the page loads 
    fetchPhotos()
}

// send a fetch request to get the photos from the back end 
// translate the response to JavaScript photo objects 
// use a method on the photo objects to append/add to the DOM 

function fetchPhotos(){
  // this line fetches the photos from the database
  fetch('http://localhost:3001/api/v1/photos')
	  // then translate the data into JSON
    .then(response => response.json())
		// then take the photoJSON object and iterate over each photo with the attributes 
    .then(photoJSON =>
		      
					photoJSON.data.forEach(photo => {  
          const attributes = photo.attributes;
          let newPhoto = new Photo(attributes.image_url, attributes.artist_name, photo.id, attributes.photo_with_comments);
					// then push the new photo objects into the allPhotos array from above 
          allPhotos.push(newPhoto); 


        })
    })
```

### Buttons, buttons, who's got the buttons? 
Now that I FINALLY (this took me several weeks) knew how to fetch data from the database I needed to use this data to create a slideshow. This was really confusing too because every slideshow tutorial I came across used a JavaScript array of image urls. I didn't realize instead of creating an array, I could use the array I had created at the top of the file `allPhotos`. Howard also helped clear up this confusion for me and helped me with creating the array.

After that I used several different tutorials and Codepens to help me get the right functionality for the slideshow. Great! The buttons were up and going within a few days which got me thinking I was really close to being done. Little did I know, I was still about 3 weeks from being finished. 

### Giving credit where credit is due 
After getting the buttons to work, I really wanted to get the artist's names with their photos to give them proper credit. I don't like anyone's work to go unmentioned so I started down the long confusing road of adding text under a photo that changed every 5 seconds of so. It was an easy fix but took days of going through the documentation to finally come up with the solution. 

1. Create the photo object with attributes, 
```
class Photo {
    constructor(imageUrl, artistName, id, photoWithComments) {
        this.imageUrl = imageUrl; 
        this.artistName = artistName;
        this.id = id;
        this.photoWithComments = photoWithComments; 
        
      }
		}
```
2. Create a render function with dynamic attributes
```
 renderData() { 
  return `
    <img src="${this.imageUrl}" height="500px" width="600px" class="slide showing rounded-corners"/> 
    <p>photo credit: ${this.artistName}</p> 
    <ul id="comments" data-id=${this.id}>  
    </ul>
    `
  
}
```

### Connecting the Comments to their Photos 

The comments feature was without a doubt the hardest part of this entire project and I'm still not 100% satisfied with the results. It took me almost 3 weeks to get this one feature right. First I looked up how to make a form in JavaScript but I wasn't getting anywhere with it. After several sessions with Annabel and several more sessions with Howard, I started to understand the process from start to finish. 

First, I needed to fetch the comments data from the database which meant a seperate fetch file. It seems obvious in hindsight but I wasn't sure I actually need a seperate fetch function. Annabel helped clear that one up for me. 
Creating the form only took about a day or so but connecting the comments to their photos took sooo long, I thought I'd never be done. 

Next, I needed to connect the comment to the photo. I thought it had something to do with the `id` but wasn't sure how to go about doing it. After going through the sessions with Annabel and Howard, I was able to get used to using `debugger` to check for what the code was doing. If you're working on your project now, I strongly recommend you learn how to use `debugger`. 

After weeks of trying to work this out, I finally was able to put it down into several steps: 
1. Create the adapter for fetching data from the database 
2. Create the comment class with attributes
3. Create the comments class with each of these functions working together to create and render the comments
 ```
 class Comments {
  constructor() {
    this.comments = []
    this.adapter = new CommentsAdapter()
    this.initBindingsAndEventListeners()
    this.fetchAndLoadComments()
     }
	}
	```
	
If you'd like to see the rest of the comments code here's (the JavaScript repository)[https://github.com/donnacamos/baby-animals-photo-generator-frontend]. 

### Review, review, review: I cannot emphasize this enough 

The best thing you can do for yourself while building this project is to review and study what each element and function is doing and how everything works together. It's the secret to getting making your project with the features you want and makes doing it again much easier the second and third time. Don't be afraid to ask for help either. I'd still be back at the fetch section of my project if I hadn't scheduled a meeting with Howard. 

JavaScript is tricky and confusing but if you learn how to use `debugger`, `console.log`, remember that the fundamental principal that all JavaScript is doing is creating variables and functions and putting them together to do a task, it makes everything much easier to read. 

Also, go easy on yourself. JavaScript is a skill most people take years to learn. I still don't fully understand everything about how my project works. Just enough to know what it's doing on a basic level. 

### Resources 
(JavaScript Repository)[https://github.com/donnacamos/baby-animals-photo-generator-frontend]
(Rails API Repository)[https://github.com/donnacamos/baby-animal-photo-generator-api]
(Cernan's Notes App Repository)[https://github.com/cernanb/notes-app]
(Rails and JavaScript Blog Post)[https://medium.com/@luoana.chirita/using-a-ruby-on-rails-backend-with-a-javascript-frontend-ddf25f8f19c6]


