---
layout: post
title:      "Voluntell: connect with the causes you love"
date:       2017-11-16 19:59:17 +0000
permalink:  voluntell_connect_with_the_causes_you_love
---


It might sound cliché, but I’ve always wanted to help people. For most of my life, I’ve tried to seek out opportunities to help, but my biggest difficulty is figuring out *how* I can help. I know there are so many struggles in the world, but I feel helpless not knowing what I can do. I was volunteering last weekend at the local humane society, and I was logging my hours on their app, but I kept feeling frustrated at how their app was laid out. It made me wonder what it would be like to build a volunteering app, and so I created Voluntell. 

Voluntell is a Sinatra app that connects volunteers with opportunities to help their favorite causes. The concept is: they volunteer and help others, then they tell their friends about it to inspire them too. Users are able to sign in or login, and see all of the opportunities available. They can create their own opportunities, read the details of each opportunity available, update their own opportunity (and only their created opportunities), and delete their opportunity for any reason. They can also search opportunities by cause and bring up any opportunity that matches their interests. 

They are can navigate to the stories page, and read all of the stories written about volunteers' experiences. They can create their own story, update their story, and delete their story. They’re also able to see their own personal page along with other volunteers’ personal pages that describe all the opportunities that they’ve posted and all of the stories they’ve written. They can edit their profile including their email and password, but all usernames are unique and only created upon creating a user/volunteer. 

So how is the code set up? I used a MVC structure- Models, Views, Controllers. I first set up the database with the following schema: 

![https://i.imgur.com/EM8bsDK.png?1](https://i.imgur.com/EM8bsDK.png?1)

I set up my models as follows: 

 ![https://i.imgur.com/GjWY9pq.png](https://i.imgur.com/GjWY9pq.png)
 ![https://i.imgur.com/Riw2ryA.png1](https://i.imgur.com/Riw2ryA.png1)
 ![https://i.imgur.com/W80COit.png](https://i.imgur.com/W80COit.png)
 
 
This would set up my associations so that my controllers and views could be created correctly. I then worked between my controllers and views to create the behavior and display of the site (set up forms, add flash messages for specific actions, etc). I would show photos of my controllers: Application Controller, Volunteer Controller, Opportunities Controller, and Success Stories Controller, but truthfully, it would make this blog unbelievably long. So, if you’re interested in any specifics of the setup, check out the source code here: 
[https://github.com/jessiehuff/voluntell-sinatra-app](https://github.com/jessiehuff/voluntell-sinatra-app)


To show you a little preview of what Voluntell looks like at the moment, I’ll give a few photos here: 
 
 ![https://i.imgur.com/4tVLTu8.png1](https://i.imgur.com/4tVLTu8.png1)
 ![https://i.imgur.com/Y5rNSFv.png?1](https://i.imgur.com/Y5rNSFv.png?1)
 ![https://i.imgur.com/FYOJuRc.png?1](https://i.imgur.com/FYOJuRc.png?1)
 ![https://i.imgur.com/espUZrW.png?1](https://i.imgur.com/espUZrW.png?1)

There are so many other photos I could show you of the site, of editing the opportunities or stories, of deleting them, the sign in and login, of logging out, etc. If you’d like to see the full application in action, clone the source code and take a look! If you’d like to see a video explanation of the app, check out the walkthrough here: 

[https://www.youtube.com/watch?v=-mmLmKrLiYU&feature=youtu.be](https://www.youtube.com/watch?v=-mmLmKrLiYU&feature=youtu.be)


While I know this is mostly the structure and functionality of a site, I am so proud of everything I’ve done with it. I had a blast building this app, and honestly, I’ll probably keep editing it. I think the next feature I’d like to add is a search by location function. Stay posted if you’d like see more! 

![https://i.imgur.com/XP1DwNA.jpg](https://i.imgur.com/XP1DwNA.jpg)
 
Me hugging my app. ![https://i.imgur.com/NPtQuFY.png2](https://i.imgur.com/NPtQuFY.png2)

