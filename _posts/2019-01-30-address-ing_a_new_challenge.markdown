---
layout: post
title:      "Address-ing a New Challenge"
date:       2019-01-30 19:41:34 +0000
permalink:  address-ing_a_new_challenge
---


I was recently given a coding challenge by a company, and my fingers were nearly twitching in excitement to get started on it. I forced myself to be patient, read the requirements and expectations clearly and then work through a plan of attack for the project. The challenge was fairly simple: create an address book out of the data received through an API. 

The backend was powered through an Express Node js server, some of which was written for me. The first part of the challenge for me was to understand this code that looked somewhat unfamiliar to me (as I haven’t used much Express Node js yet), decipher what its purpose was, and then extend it to my goals. I needed to make sure the file structure was clear and straightforward so I created a new folder for the home page when the application was loaded and created a file for the JavaScript logic: index.js, a file for the html structure: index.html, and a file for the CSS styling: style.css. However, I had to specify in the server.js file that I was using these files in this way with the express node format, like so: 

![https://i.imgur.com/gLktS3Y.png](https://i.imgur.com/gLktS3Y.png)
 
 
It was slightly tempting for me to jump back into my comfort zone of using React as it’s currently my favorite to program in, but I decided to challenge myself and refresh my knowledge on straight JavaScript and jQuery. 
I modeled my index.html file on the company’s mockup given. However, their original html was written statically with examples typed in instead of pulled from the data so I mostly used their naming conventions in the html structure but removed all of the static information. Most of my work was done within the index.js file as I began thinking through the logic of how the application would function. 


Since a page can’t be manipulated safely until the document is “ready”, I included the `$(document).ready` function to detect this state of readiness once the page Document Object Model (DOM) is ready for the JavaScript code to execute. In this function, I executed my first function that loads the index of all available contacts on the left panel of the screen and loads the first person in the address list’s information on the right panel when the page loads. 

My loadPeople function executes an ajax call to the API, sorts the address contacts alphabetically, appends a letter head when it’s a new, unique first letter used, and attaches the event listener to each contact name (when each name is clicked, the right panel loads their information). 

![https://i.imgur.com/phmwebg.png](https://i.imgur.com/phmwebg.png)
 
 ![https://i.imgur.com/SJCansU.png](https://i.imgur.com/SJCansU.png)
 
 
This creates the following in the left panel of the page: 

![https://i.imgur.com/qipWn1S.png](https://i.imgur.com/qipWn1S.png)

 
From there, I used jQuery to select these items, and when they are clicked, pass their id to the loadPerson(id) function. This function does another ajax call for that specific item in the database, clears whatever data was already showing on the right panel with the `.remove()` method, and then appends the new data to the page with the `.append()` method. (Ex: `$(‘.wrapper’).append(“<div class=’education-date’>” + edu.startYear + ‘-‘ + edu.endYear + “</div>”) `)


That’s pretty much all there is to the JavaScript/jQuery section. You do need to add a little bit of CSS to get it to look the way you want, but a good one to remember for this app was: `display: inline-block;` which allows you to set a width and height on the element if you choose to, the top and bottom margins/paddings are respected, and it does not add a line-break after the element so the element can sit next to other elements. With some added CSS and a default profile photo url added, our finished product looks like this: 

 ![https://i.imgur.com/ofoBNUA.png](https://i.imgur.com/ofoBNUA.png)
 
 
 
It took me some time to get the CSS exactly the way I wanted, and it’s still an area that I want to grow further in. The night before I finished this project, I was so frustrated that I was having trouble getting it exactly the way I wanted, despite working on it for hours. I eventually decided to stop and go to bed. The next morning, I finished it and got it working within 20 minutes. Sometimes the best thing you can do to get over a hurdle is to just take a break and maybe get some sleep. Sleep is a beautiful thing for the mind. 


 
![https://i.imgur.com/usrsvLQ.jpg](https://i.imgur.com/usrsvLQ.jpg)
