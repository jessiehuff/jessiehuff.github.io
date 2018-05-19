---
layout: post
title:      "Refining Crux"
date:       2018-05-18 21:58:00 -0400
permalink:  refining_crux
---

If you’ve been following my blog for a while, you may notice that I’m a big fan of communication and connection. I’ve noticed that proper communication is a major issue for countless organizations which is what inspired my last blog and project- Crux. 

If you missed that blog, you can read it here: [http://jessiehuff.com/crux_making_communication_simpler](http://jessiehuff.com/crux_making_communication_simpler)

Since creating the project management application, it was time to give it more functionality with some JavaScript. First on the list of things to do is to stop redirecting or doing page refreshes and start rendering via jQuery and an Active Model Serialization JSON Backend. Which essentially means some pretty AJAX requests, the backend rendering the items in JSON format and then appending them to the page or submitting the forms. I also translated the JSON responses into JavaScript Model Objects. 


I started off my JavaScript with some event listeners: 

 ![https://i.imgur.com/tR15uur.png](https://i.imgur.com/tR15uur.png)
 

And subsequently went through each of the events that I wanted functionality on. To show an example, I’ll show the message object: 

![https://i.imgur.com/fkCpPep.png](https://i.imgur.com/fkCpPep.png)
 
 

And finally, I added a “Next Project” feature so that users could cycle through each project’s show page for added convenience. A little long, but quite beautiful if I do say so myself. (I know, I know, I’m a total nerd, but I’m proud to be one.) 
 
 ![https://i.imgur.com/8vchT7K.png](https://i.imgur.com/8vchT7K.png)
 ![https://i.imgur.com/BRMNjfD.png](https://i.imgur.com/BRMNjfD.png)
 


I know that’s a pretty quick summary of my JavaScript functionality, but I learned so much about the nuances of JavaScript, jQuery, and AJAX. I think what took the longest was always making sure that everything matched up, that I was selecting exactly what I wanted, and making sure my syntax was what it needed to be. There were plenty of moments of frustration before complete realizations that I was attempting to select a class instead of an id or vice versa. So, reminding myself to be completely thorough with my identifiers was enlightening.  


Overall, I still have so many dreams and ideas for this project that I could spend days perfecting it. I’m hoping to add some additional CSS at some point soon so that it looks just as awesome as its code. It seems that there’s always more that can be done, but for now, I’m excited about how this project came together. 

