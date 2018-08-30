---
layout: post
title:      "localStorage Storing Errors"
date:       2018-08-30 03:57:24 +0000
permalink:  localstorage_storing_errors
---


This error was the bane of my existence for far too long. 

![https://i.imgur.com/JCKMEW3.png?1](https://i.imgur.com/JCKMEW3.png?1)
 
 
Seems like a relatively harmless error, right? You might think, well, `props.events` probably isn’t an array which is why map isn’t working. Which, you’d be right, but I was more concerned with what would cause something that previously worked to suddenly break. Even if I worked around it and forced that code back into an array, there seemed to be a strange ripple effect of new errors in my code. Looking into it further with some debugging, somehow my state was changing from initially being defined as an array to an object, which was throwing errors throughout my code. So, my question was- what would change my state from an array to an object?


Scouring the internet, I was at wit’s end. It seemed that no matter what I changed, my error wasn’t going away. Even if I reset my entire database, the error persisted like a bad cold. I asked countless others, posted on forums, but no one seemed to have any clue what was happening with my program. Even more mysterious, when someone else cloned down my project, the errors didn’t appear on their side. I decided it had to have something to do with my operating system and switched from Windows to Linux since I’ve gone back and forth between both anyway. Everything was good for a while, maybe a day where I was at bliss. Until the phantom error reappeared, and I was stuck on both operating systems. I thought I was going to go insane over this error, and nothing I found online seemed helpful. 


After spending too much time on it, I finally figured it out and wanted to share in case this ever happens to anyone else. If you’re struggling through an error that won’t go away or an error with React state, maybe this can be the article that I wish I’d found earlier. 


Let’s start with the state. This one I’m almost embarrassed to admit, but while I set my state as an array in the beginning, I treated it like an object later in my reducer, which made the browser interpret state as an object instead of the intended array. 


So, let’s say I started off like this in my reducer: 

![https://i.imgur.com/g1q5Kho.png](https://i.imgur.com/g1q5Kho.png)


I was initially writing my cases as though state was an array which makes sense. But then I wanted to add photos too, and photos are a nested association within my backend. So, I wrote my add photo case like this (after adding photos to the initial state): 

![https://i.imgur.com/N5TyNOE.png](https://i.imgur.com/N5TyNOE.png)

Yeah, right off the bat you can see that I treated it like an object. So easy fix, right? It definitely should be, but it seemed that no matter how I changed my state in my reducer, my error wasn’t going away. Well, I recently added localStorage to my program which is similar to sessionStorage, but it’s persistent across sessions so whenever you close your browser and open it again, the fetched result from the API should still be available. You might already see where this is going. 

Due to the fact that my data was being stored in localStorage, no matter what I changed in my code and how many times I restarted my server or emptied my database, my local storage kept it saved for me on my browser. That’s also why others couldn’t replicate my error. I’d already fixed the state error which showed on their side, but it didn’t show on mine because it continued to pull from local storage. To clear this, I just had to go into my developer tools, go to the Application tab, find Local Storage on the left-hand side, right click it, and hit “clear.” Easy as that, but a pain in the butt to have an issue with. 

 ![https://i.imgur.com/CGc3eWk.png](https://i.imgur.com/CGc3eWk.png)

In the end, it was a simple fix that caused me so much grief, but I’ve become nearly religious now about checking my storage and making sure I know where the application is pulling its information from. So, if you have a persistent error that seems completely immune to anything you do and you’re currently using localStorage, make sure to clear it and then make your changes so you don’t end up in the cycle of frustration I was in. 

![https://i.imgur.com/rdstIOf.png](https://i.imgur.com/rdstIOf.png)
 

