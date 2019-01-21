---
layout: post
title:      "To Redux or Not to Redux"
date:       2019-01-21 12:43:46 -0500
permalink:  to_redux_or_not_to_redux
---


As someone who loves React, there’s often the question of whether to add Redux to your React application. There are a lot of reasons to include Redux so I’d like to go over what Redux does and why you might want to use it. 


**Overview of Redux**:  
Redux is a state management tool that enables you to keep your state in a store and each component can access the state that it needs from this store. 
* Has a central store that holds entire state of the application 
* Each component can access the stored state without having to send down props from one component to another 
*  ** Building parts**: actions, store, and reducers (which we will review below) 


**Actions**:  
Actions are the way you send data from an application to the Redux store. This can be from user interactions, API calls, or form submissions. Actions are sent using the store.dispatch() method, but these actions are just plain JS objects and must have a type property to indicate the type of action to be carried out. They also must have a payload that contains the information that should be worked on by the action. 

Example: 
 
 ![https://i.imgur.com/gMliT5r.png](https://i.imgur.com/gMliT5r.png)
 
**Takeaway Points**: 
* The way you send data from application to Redux store (can be from user interactions, API calls, or form submissions) 
* Actions sent using store.dispatch() method
* Actions are plain JS objects and must have a type property to indicate the type of action to be carried out
* Must also have a payload that contains the information that should be worked on by the action. Actions are created via an action creator 

https://redux.js.org/basics/actions 


**Reducers**:  
Reducers specify how the application’s state changes in response to actions sent to the store. Reducers are pure functions that take the current state of an application, perform an action and return a new state. These states are stored as objects, and they specify how the state of an application changes in response to an action sent to the store. As pure functions, they do not change the data in the object passed to it or perform any side effect in the application. Given the same object, it should always produce the same result. You should never mutate a reducer’s arguments, perform side effects like API calls, and routing transitions, or call non-pure functions (e.g. `Date.now()` or `Math.random()`) 

Example: 

![https://i.imgur.com/N4biTvO.png](https://i.imgur.com/N4biTvO.png)

 
**Takeaway Points**: 
* Pure functions that take the current state of an application, perform an action and returns a new state 
* These states are stored as objects and they specify how the state of an application changes in response to an action sent to the store 
* As pure functions, they do not change the data in the object passed to it or perform any side effect in the application. Given the same object, it should always produce the same result

https://redux.js.org/basics/reducers 




**Store**: 
The store holds the application state, and there will only be one in any application. You can access the state stored, update the state, and register or unregister listeners via helper methods. Whereas the actions represent the facts about “what happened” and the reducers update the state according to those actions, the store is the object that brings them together. 

**Takeaway Points**: 
* Holds the application state, only one in any application 
* Allows access to state via `getState();` 
* Allows state to be updated via `dispatch(action);`
* Registers listeners via `subscribe(listener);`
* Handles unregistering of listeners via the function returned by `subscribe(listener)`

Example: 

![https://i.imgur.com/N80FBZ8.png](https://i.imgur.com/N80FBZ8.png)
 
 
Bear in mind that in my example above, I also implement Thunk Middleware. The Redux docs uses a much simpler example that might be better to follow for more simple applications: 

![https://i.imgur.com/isKSaaw.png](https://i.imgur.com/isKSaaw.png)
 
 
https://redux.js.org/basics/store 


**When to use Redux** 

In React, state has to be passed from one component to another until it gets to where it is needed. State will have to be lifted up to the nearest parent component and to the next until it gets to an ancestor that is common to both components that need the state and then it is passed down. This makes the state difficult to maintain and less predictable. It also means passing data to components that do not need such data. 
State management gets messy as the app gets complex. A state management tool like Redux makes it easier to maintain these states. 

**When do you start using Redux?** 
1. Same piece of application state needs to be mapped to multiple container components (ex: session state) 
2. Global components that can be accessed from anywhere (ex: show notifications, snackbars, tooltips, modals, interactive tutorials, etc). Without Redux you would need some other event system or have to instantiate the component every time it gets used.
3. Too many props are being passed through multiple hierarchies of components (ex: happens a lot with wrapper components that just provide layout styles but don’t require a lot of data or configuration, more practical to side-chain Redux directly into a lower-level component) 
4. State management using setState is bloating the component (components that are over several hundred lines of code start to become harder to reason and maintain, separating out the state management into a reducer breaks up the code and makes it more readable) 
5. Caching page state (to avoid calls to the backend) 


**Benefits of Using Redux**: 
1.	Redux makes the state **predictable**- if the same state and action are passed to a reducer, the same result is always produced as reducers are pure functions
2.	**Maintainability**- Redux is strict about how code should be organized which makes the structure of any Redux application easier to understand and maintain 
3.	**Debuggable**- by logging actions and state, it is easy to understand coding errors, network errors and other forms of bugs that might come up during production 
4.	**Ease of testing**- easy to test Redux apps as functions used to change the state of pure functions 
5.	Can use **local storage** to persist some of app’s state
6.	Can be used for **server-side rendering**. You can handle the initial render of the app by sending the state of an app to the server along with its response to the server request. The required components are then rendered in HTML and sent to the clients 


**Resources: **

https://redux.js.org/basics/basic-tutorial 

https://medium.com/@fastphrase/when-to-use-redux-f0aa70b5b1e2

https://blog.logrocket.com/why-use-redux-reasons-with-clear-examples-d21bffd5835


