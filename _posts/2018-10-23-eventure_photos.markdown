---
layout: post
title:      "Eventure Photos"
date:       2018-10-23 20:19:42 +0000
permalink:  eventure_photos
---


After a lot of studying and trial and error, I’ve created a really cool application that I’m proud of called Eventure Photos. It’s a Rails API backend with Redux middleware and a React/JS frontend. Eventure Photos allows everyone at an event, whether it’s a meeting or a wedding, to share their photos in real time. With so many of my friends and colleagues wanting to share their event photos as they happen, this application was the perfect solution. I definitely had to expand my knowledge a lot to finish this project, but it’s really made me fall in love with these technologies. 


I could write countless articles about the things I’ve learned from this project. So, for this post, I’ll just be going over the overview for brevities sake. It seems best to try to break specific aspects of the project up, staying in the theme of React and its component framework. Stay tuned for upcoming articles for more!


I began by setting up my application with this article in mind: https://www.fullstackreact.com/articles/how-to-get-create-react-app-to-work-with-your-rails-api/


Essentially, I needed an API server and a Webpack dev server so I used Foreman to help with this endeavor. The create-react-app provides a mechanism for working with an API server in development. We can have the Webpack development server proxy requests intended for our API server like this: 


![https://i.imgur.com/7v5jI4T.png?1](https://i.imgur.com/7v5jI4T.png?1)


Foreman is a utility for managing multiple processes, and it will allow us to boot each of our desire processes. For a more detailed explanation on how to set this up, check out the link from Anthony Accomazzo above as he does a great job going through it step by step. 


The next phase of this project was setting up the structure, organization, and planning. I spent some time constructing the database essentially so that events would have the attributes of name, description, and a cover photo whereas photos are comprised of filenames. The reason I made events and photos as separate objects is I wanted them to have a separate life cycle from each other. I also implemented Active Storage for the cover photo and attached photos. The process of learning how Active Storage interacts with React and Redux was quite an endeavor so I intend on writing a blog post on that specifically soon. 


However, to summarize, I followed the Active Storage docs by utilizing a local storage system, made sure to specify that that the event model `has_one_attached :cover` and likewise with photo. I then made sure that the form had the proper sections and an event handler to handle both a change of text or an uploaded file. 


I used redux-thunk as it is a middleware that looks at every action that passes through the system, and if it’s a function, it calls that function. In addition, all container components need access to the Redux store so they can subscribe to it. I used the React Redux component called <Provider> to make the store available to all container components in the application without passing it explicitly. You only need to use it once when you render the root component. For my application it ended up looking like the following after implementing all components (bear in mind that it is specifically adapted to the rest of my code, particularly throttle): 

![https://i.imgur.com/4uUOUoC.png](https://i.imgur.com/4uUOUoC.png)

 
I then began working on the React components. I organized these files based on Dan Abramov’s presentational vs. container component organization. If you’re unfamiliar with this concept, I highly recommend his article on the subject: https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0


An easy way of explaining whether or not a file should be considered presentational or container is does it need to be aware of the state or is it just displaying something? If it needs to be aware of the state (let’s say through a mapStateToProps function), it will likely need to be a container. I’ll go through a brief example of how these components flow from one to another. 


First, we should start in the App.js file where specify our routes on the React side. On my Rails API side, my routes.rb file is the following: 

 ![https://i.imgur.com/TWSYnjM.png](https://i.imgur.com/TWSYnjM.png)
 
 
On the React side they are: 

![https://i.imgur.com/gcpe2rt.png](https://i.imgur.com/gcpe2rt.png)
 
 
Now that we’ve defined our routes, let’s give an example of creating a new event. 

 ![https://i.imgur.com/H9kCr3X.png](https://i.imgur.com/H9kCr3X.png)
 
 
In our EventsNew.js file, we define what attributes we would like our React side to be aware of, in this case: name, description, cover (which will be a file), and an id. Then we need to create a form for a new event. 

![https://i.imgur.com/GxTTZgR.png](https://i.imgur.com/GxTTZgR.png)


As you can tell, there are event handlers for onChange and onSubmit for the form. We now need to write specific handlers for text changes, file uploads for the cover, and a submit handler. 

![https://i.imgur.com/4HNvd8J.png](https://i.imgur.com/4HNvd8J.png)

 
To work upwards, the handleFile event handler is essentially telling your program to set the cover in the state to this specific file. Likewise, the handleOnChange takes the name of whichever form field and sets it to the value in that form field. When the user submits the form, we first prevent the default so that we can send this information to our actions.js file to addEvent. Whenever it finishes with this, it will push to the events page. Don’t forget to connect these at the end of the file! 

`export default connect(null, { addEvent })(EventsNew);` 

On the index.js page under actions, we then need to define the addEvent action. What we need to do is take the values we just put into the event form, attach it to something the database can use, post it to the database, and then adjust our state accordingly. So, what I found to be most helpful in this endeavor was formData. If you need to familiarize yourself with formData first, I highly recommend looking into it. 
https://developer.mozilla.org/en-US/docs/Web/API/FormData/Using_FormData_Objects 


![https://i.imgur.com/CwRQa9e.png](https://i.imgur.com/CwRQa9e.png)



So, as you can see, we pass the values that we put into the form fields into this function. We create a formData object called eventData, append all of the relevant information to eventData, fetch the specific route from the backend (in this case `http://localhost:3000/api/v1/events`), use the method ‘post’, set the body to eventData, and then create promises to return the data as json and to dispatch the event to the reducer to affect the state. 


Now, remember, the cover should be a file so if you throw a debugger into this function, `values.cover` should look like this: 

![https://i.imgur.com/y5OiPXC.png](https://i.imgur.com/y5OiPXC.png)

 
I set up the photos the way that the Active Storage docs specified, however I needed a serializer to make sure that I could control how the event would be serialized. If you set up the backend for attachment correctly it should look something similar to the following in your terminal: 

![https://i.imgur.com/8Xj70lu.png](https://i.imgur.com/8Xj70lu.png)
  
	
Basically, you should be seeing it create something in active storage. In the event serializer, you need to specify how you want the front end to get this data. Now remember, for photos, you’re going to need a url to display the image. In order to do that, I did the following: 

![https://i.imgur.com/NVZIUTM.png](https://i.imgur.com/NVZIUTM.png)
 
 
I specified the attributes I wanted to serialize and then I defined how to produce the url for the image. Once this data has been sent to the backend, serialized, and sent back to the frontend, we then get sent to the reducer. In the reducer, we need to first specify how you want to structure your state and create a switch for different potential actions. For my state, I made it an object that had two arrays: events and photos. The reason I made these separate arrays is because of the concept of normalizing state shape. For further explanation on that, see the Redux docs: https://redux.js.org/recipes/structuringreducers/normalizingstateshape
 
 
 ![https://i.imgur.com/jtgH7Wj.png](https://i.imgur.com/jtgH7Wj.png)
 
 
In my ‘ADD_EVENT’ case, I first returned the current state, and then I specified that I wanted to add this new event to the array of events in the state. From there, that should essentially be it. The user is able to fill out the form fields, dispatch the action, send formData to the backend, serialize this information, send it back to the frontend, and affect the Redux state through the reducer. 
A finished event page (after setting up the page format, making it possible to add photos with a similar process, etc) would look like the following: 

![https://i.imgur.com/1Q74lWL.png](https://i.imgur.com/1Q74lWL.png)


All of this is a very simple explanation of this process, but I understand that if you’re new to all of this, it might seem a little overwhelming. My best advice if you’re starting a project like this is to break it into manageable chunks. As you get each of those sections working, celebrate each of those wins. Make sure you understand each individual concept you’re using. As you study the concepts, the flow will begin to make much more sense. And debugging is far easier when you understand how the components flow from one to another. 


If you’re struggling, don’t hesitate to reach out to people to ask questions. I’ve discovered that even strangers are sometimes extremely willing to lend a helping hand. I’m constantly blown away by how amazing the developer community is. If you have any questions, please don’t hesitate to reach out to me! I’d love to help you through these concepts or expand on them further if they don’t quite make sense yet. 


Happy coding! 

![https://i.imgur.com/2jpw5kP.jpg](https://i.imgur.com/2jpw5kP.jpg)
 

