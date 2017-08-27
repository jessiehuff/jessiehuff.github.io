---
layout: post
title:  "Flexing Our Capabilities With Flexbox"
date:   2017-08-26 20:56:02 -0400
---


I am relentless. 

This usually works in my favor, even though it might annoy my friends and family when my brain is currently working through a problem. I was told this past week that I reminded someone of *The Accountant*, a movie about a determined mathematician. I just needed to solve that lab problem.

We were essentially given a website mockup and told to use what we knew in HTML and CSS to design the content accordingly. Simple enough, right?  Yet, I could not get my code to display the way I wanted it to, and I spent hours working out the minute details- adjusting element widths, adding margins, creating columns and rows, applying a clearfix to parent elements. 

As I was trying to look at my code in my browser, the format never changed. No matter how I changed my code, the website looked the same. I discovered that sometimes the browser will cache the website’s code to save time in accessing it in the future. After my first look at the website, my browser kept refreshing the same cache of information, never updating with the new code. A quick clearing of the cache and a hard refresh did just the trick. 
Still, one of the rows was misbehaving so I worked with a few other people to see if a second, third, or fourth pair of eyes could spot the bug in my code. 

![](http://i.imgur.com/bXZWop1.jpg?3)

It was a frustrating night to say the least, but eventually we came up with a solution!

![](http://i.imgur.com/EFrb6fQ.png)
 
Ah, inline-flex, a new favorite of mine and fairly new to CSS3. It essentially made the container behave like an inline element and FINALLY solved my frustrations. Fellow developers, check out CSS Flexbox Layout (officially called CSS Flexible Box Layout Module). The main characteristic of the flex container is its ability to modify the width or height of its children to fill the available space in the best possible way on different screen sizes. (Seems excellent to use for responsive design!) If any of you are interested in learning how cool this stuff is, check out this guide I found to CSS3 Flexbox Properties: [](https://scotch.io/tutorials/a-visual-guide-to-css3-flexbox-properties#toc-flexbox-container-properties)
