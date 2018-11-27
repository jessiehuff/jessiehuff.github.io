---
layout: post
title:      "Actively Learning with Active Storage"
date:       2018-11-27 19:40:29 +0000
permalink:  actively_learning_with_active_storage
---


“Paperclip is deprecated?” I groaned. I was right in the middle of working on my photo uploading application, Eventure Photos, that’s equipped with a Rails API back-end, Redux middleware, and a React / JavaScript frontend. (See my post about its overview [here.](http://jessiehuff.com/eventure_photos)) I was planning on using the Paperclip gem that was previously in vogue for my photo uploading, but with its deprecation and replacement by Active Storage, it made much more sense to just learn Active Storage. 

Alright, no big deal, I’m pretty used to learning new technologies so I wasn’t too concerned about it. What I didn’t realize though is that because Active Storage was so new, there was very little documentation on how it interacted with React or anything other than the normal Rails stack. So, without many hints from my beloved Internet searches for my quest, I ventured out to discover the answers that evaded me. In other words, a lot of experimentation, talking to my computer hoping that I could convince it to fix my code for me, and lots of walks in between my failed computer persuasion. 

Alas, I finally figured out how to get it working so I’m here to share it with anyone else on that quest. Bear in mind that your code may be different than mine and therefore may have some differences in implementation, but hopefully by reading this article, you’ll at least get a better understanding of Active Storage. 


How I felt when I got it all working: 

 ![https://i.imgur.com/HBU1lZi.jpg](https://i.imgur.com/HBU1lZi.jpg)
 
 
 

What is Active Storage? 

In the words of the official Rails documentation: “Active Storage facilitates uploading files to a cloud storage service like Amazon S3, Google Cloud Storage, or Microsoft Azure Storage and attaching those files to Active Record objects. It comes with a local disk-based service for development and testing and supports mirroring files to subordinate services for backups and migrations.”



Basic documentation: 

https://edgeguides.rubyonrails.org/active_storage_overview.html 

Now I highly recommend starting there with the basic documentation. It explains how to set up Active Storage, choosing a storage location, attaching files on the rails side, removing files, direct uploads, etc. I’m also excited to see that it looks like they’ve recently added slightly more in terms of linking and image transformation with MiniMagick. 

So, to summarize some of the basics they present, Active Storage uses two tables in your application’s database named active_storage_blobs (that store your files information, i.e. file type, file name, etc.) and active_storage_attachments (that stores that actual file). You are going to need to pick a place to store your information: local, Amazon, Google etc. I chose local for my application as it’s free and easy. 

(If you are in production, however, you may not have a choice. Heroku, at least, doesn’t give you a hard drive to save files to, so you’ll have to use S3 or Google Cloud Platform. Even if you’re hosting somewhere where it’s possible, it’s probably cheaper to use a dedicated storage provider like S3.) 



To help me fully understand how everything connected, I reached out to Cameron Bothner (a Web Application Developer at the University of Michigan who recently created his own gem for Active Storage and React usage: react-activestorage-provider) and discussed his experience with using Active Storage and React. He gave me an excellent explanation that I’d like to include here. 

> Using ActiveStorage outside of a pure Rails view, it foregrounds a decision that you would otherwise be able to postpone: do you need direct upload? Without direct upload, your users submit files (e.g. profile image) to your app at the same time and to the same API endpoint as the rest of their submission (name, bio, etc). Rails handles the file for you, and when you do `@user.update(user_params)` the file is automatically transformed and sent off to the storage service (like S3) you're using. It's definitely the simpler choice, but you can run into problems with larger files or if your users have slower connections. Since your app has to receive the file upload and reupload it to S3 all within one request cycle, it's possible that it will time out if you're on Heroku or similar providers, since they have a limit for how long a request can take.
> 
> To get around that, they added capacity for Direct Upload, which basically goes like this: your user (a.k.a. your React app, on behalf of your user) says "hey, I've got a file. Where should I put it?" And your Rails app prepares a Blob record in your database, figures out where in S3 it would upload the file, and then says to your front end "put the file here and call it by this id." The user then uploads the file to Amazon directly. At this point, your app has a Blob record that points to a file, but that Blob is free-floating, not attached to any of your models. So then your user submits their profile information, but for image all they send is the id corresponding to the already uploaded file. That's when your app attaches the free-floating Blob to the User object.
> 
> From inside an ERB view, with Rails' unobtrusive JavaScript, changing from in-request upload to direct upload is as easy as adding `direct_upload: true`. But from React you have to do all that stuff by yourself, which is why I made `react-activestorage-provider`. 

Cameron was so nice to talk with me about it, and he definitely seems to be contributing to the development scene so I wanted to make sure I give him and his gem some kudos. If any of you want to implement direct upload with React, make sure to check out his gem. 

Alright, now that we have a basic understanding of what Active Storage is and does, and we’ve made our decisions about where to store the information and whether we’ll need direct upload or not, it’s time to finally get to coding!

Let’s start with the back-end first: 

In our event model, we have to let our program know that we want a cover photo attached for each event with `has_one_attached :cover`. This macro sets up a one-to-one mapping between records and files. (I also set my event’s cover attribute as a string type in my database to accept the file name.)


 ![https://i.imgur.com/WF6knfa.png](https://i.imgur.com/WF6knfa.png)



In our events controller, it will be much like you’ve probably seen before. You can include the file in your mass assignment, and Rails will take care of the attachment. Your create action can still remain simple. 


 ![https://i.imgur.com/Yemv4DJ.png](https://i.imgur.com/Yemv4DJ.png)
 
 
 ![https://i.imgur.com/G0MGw7W.png](https://i.imgur.com/G0MGw7W.png)
 
(More on the line `render json: @event` later.) 


Easy Peasy. Ok, now that we have the backend architecture set up, let’s take a look at our React frontend. Let’s start with setting initial state and our constructor. We’ll need to use state here so that we can save what the user has entered into the form fields and send it to the backend. Remember that the constructor for a React component is called before it is mounted. When implementing a constructor for a React.Component subclass, you should call `super(props)` before any other statement. Otherwise, `this.props` will be undefined in the constructor, which can lead to bugs. 

![https://i.imgur.com/Y3rghmj.png](https://i.imgur.com/Y3rghmj.png)

 
Here we’re just setting the initial state to blank strings for each attribute and an empty null object for the cover. Let’s consider the form where we’re adding the event. We’ll need fields for all of the event attributes and event handlers for when these fields are changed/submitted. 
 
 
 ![https://i.imgur.com/ypjvc48.png](https://i.imgur.com/ypjvc48.png)
 
 
So, as you can see from the above code, the field for the form will need a type defined as file and a specific file event handler. Let’s take a look at the event handlers we’ll need for this form now. 

![https://i.imgur.com/biPbRt5.png](https://i.imgur.com/biPbRt5.png)
 
Let’s start with the simplest, handleOnChange. This event handler will take the attribute fields like name and description, along with their inputted values, and set the key/value pair in the state to these values. (Ex: We set the state to- name: “The Royal Wedding”, description: “Prince Harry and Meghan Markle”) 

A similar thing is happening in the file event handler except that we’re specifically telling our program that we want the file, not just a value. 

Since we want to handle this form in a custom way, we’re going to prevent the default in the submit button. Then we’re going to send the attributes we saved in state (from the form) and send it to the addEvent action. (This is if you’re using Redux for managing state. If you are just using React, you can use your fetch request or axios directly in the event handler.)

Don’t forget this line at the end of your file!
`export default connect(null, { addEvent })(EventsNew);`

 ![https://i.imgur.com/VBC2649.png](https://i.imgur.com/VBC2649.png)
 
 
In our action, we’re going to use [formData](https://developer.mozilla.org/en-US/docs/Web/API/FormData/Using_FormData_Objects) to compile the key/value pairs we want to send as an object to our database. And then we dispatch it to our reducer to add it to state. 

![https://i.imgur.com/InCN6h8.png](https://i.imgur.com/InCN6h8.png)
 
However, once we’ve sent this information to the backend, how can we make sure that the JSON response includes the url of the attached image? I used `active_model_serializers` to specifiy how you want the front end to get the data.

![https://i.imgur.com/yVpkQJ3.png](https://i.imgur.com/yVpkQJ3.png)

 
This was one of the trickiest parts of setting up Active Storage with React. You’ll have to use `include Rails.application.routes.url_helpers` in your serializer and then define how your program will get the cover url. The Active Storage docs now cover `rails_blob_path` and `url_for`, but what worked for me is creating a variant of the image (you will need to make sure you have MiniMagick installed to get this to work), setting a general size I wanted, and then taking the `rails_representation_url` of that variant. From there, you can use the cover_url on your front end like any other attribute. For example, I used it in my EventDisplay component below. All I needed to do was place it in an image tag: `<img src={cover_url} alt=”event cover”></img>` which pulls the cover_url directly from our props. 

![https://i.imgur.com/PvWFS7n.png](https://i.imgur.com/PvWFS7n.png)
 

And that’s it! You now should have a pretty image showing on your React frontend that’s persisted in your database. 

![https://i.imgur.com/Z3xJoQR.png](https://i.imgur.com/Z3xJoQR.png)
 
Time to resume our awesome coder lives like this guy: 

![https://i.imgur.com/hX9ZzxV.png](https://i.imgur.com/hX9ZzxV.png)
 

