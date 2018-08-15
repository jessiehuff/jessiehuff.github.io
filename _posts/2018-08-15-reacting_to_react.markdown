---
layout: post
title:      "Reacting to React"
date:       2018-08-15 15:32:53 +0000
permalink:  reacting_to_react
---


Now that I’ve been working with React for quite some time, I have to say that I can understand why it’s become so popular. It’s taken me awhile to truly get my feet wet working with it, but I’ve really been enjoying it. So, I figured I’d go through some of the things I’ve learned to both solidify my understanding and maybe help anyone else out there still learning. A lot of what I put into these blogs are my own thoughts and notes, but honestly, if you’re a beginner, I really do recommend you read through the React docs themselves. It really dives deeper into every topic that you just can’t put into one blog post without being a little excessive. Every time I learn a new language, I inevitably find myself diving into the documentation to really understand it. It’s intimidating, but sometimes it really is the best way to fully understand it.

[https://reactjs.org/docs/hello-world.html](https://reactjs.org/docs/hello-world.html)



What is React? 

**React** is a declarative, efficient, and flexible **JavaScript library** for building user interfaces. It lets you compose complex UIs from small and isolated pieces of code called “**components**.” A component takes in parameters (called props or “properties”) and returns a hierarchy of views to display via the render method. The render method returns a description of what you want to see on the screen. React takes the description and displays the result. In particular, render returns a React element, which is a lightweight description of what to render. 

Example: 
```
class ShoppingList extends React.Component {
render() {
    return (
      <div className="shopping-list">
        <h1>Shopping List for {this.props.name}</h1>
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}
```


**The React Component Lifecycle **

React enables us to create components by invoking the React.createClass() method which expects a render method and triggers a lifecycle that can be hooked into via a number of lifecycle methods. 


**Breakdown of the Lifecycle: **

-	Initialization: 
* **Initial**- constructor() 
* **GetDefaultProps**- can be used to define any default props which can be accessed via this.props 
* **GetInitialState**- method enables to set the initial state value, that is accessible inside the component via this.state
```
getInitialState: function(){
    return { /* something here */};
}
```
* **ComponentWillMount**- is called before the render method is executed. It is important to note that setting the state in this phase will not trigger a re-rendering. 
      	The render method returns the needed component markup, which can be a single child component or null or false (in case you don’t want any rendering). This is the part of the lifecycle where props and state values are interpreted to create the correct output. Neither props nor state should be modified inside this function. The render function has to be pure, meaning that the same result is returned every time the method is invoked. 
* **Render** 
* **ComponentDidMount**- called as soon as the render method has been executed. The DOM can be accessed in this method, enabling to define DOM manipulations or data fetching operations. Any DOM interactions should always happen in this phase not inside the render method. 




**Props Changes-** any changes on the props object will also trigger the lifecycle and is almost identical to the state change with one additional method being called 


* **Updating Props**
* **ComponentsWillReceiveProps**- only called when the props have changed and when this is not an initial rendering. Enables to update the state depending on the existing and upcoming props, without triggering another rendering. One interesting thing to remember here is that there is no equivalent method for the state as state changes should never trigger any props changes.
```
componentWillReceiveProps: function(nextProps) {
  this.setState({
    // set something 
  });
}
```
* **ShouldComponentUpdate**: This function is called as shouldComponentUpdate(nextProps, nextState) and must return a boolean. If you're super concerned with wasted renders this is a place where we could think about improving performance.
* **ComponentWillUpdate** (rarely used, cannot call setState)
* **Render**  
* **ComponentDidUpdate**- This can be used in scenarios where you want to make changes to the DOM after the the component is updated. For example think about if you were using a library like masonry that allows you to rearrange blocks based on sizes etc you could use componentDidUpdate to access the DOM after the layout is set. Additionally could be used for any calls to the database you would to have run only after an update is completed.

 ![https://i.imgur.com/y3PThnB.png?1](https://i.imgur.com/y3PThnB.png?1)
 
 
 ![ ![](https://i.imgur.com/RZLOssa.png?1)
](https://i.imgur.com/RZLOssa.png?1)


![https://i.imgur.com/cPmuJCF.png](https://i.imgur.com/cPmuJCF.png)
 

If you’re new at these concepts, it really will just take some repetition and practice to fully integrate it into your arsenal. This blog is really just an overview of these concepts so I highly recommend reading more to familiarize yourself with React and also playing with it on your own. I’m currently working on my own React project which has really helped me understand the concepts. I’ll leave some resources below to some of the sites I used to better understand React so hopefully they’ll help you too. 

**Resources: **

[https://reactjs.org/docs/hello-world.html](https://reactjs.org/docs/hello-world.html)	
[https://reactjs.org/tutorial/tutorial.html ](https://reactjs.org/tutorial/tutorial.html )
[https://engineering.musefind.com/react-lifecycle-methods-how-and-when-to-use-them-2111a1b692b1](https://engineering.musefind.com/react-lifecycle-methods-how-and-when-to-use-them-2111a1b692b1)
[https://reacttraining.com/react-router/web/guides/philosophy](https://reacttraining.com/react-router/web/guides/philosophy)
[https://gist.github.com/alexgriff/1b5850cac9a1d565f0cb66a941505b99](https://gist.github.com/alexgriff/1b5850cac9a1d565f0cb66a941505b99)





