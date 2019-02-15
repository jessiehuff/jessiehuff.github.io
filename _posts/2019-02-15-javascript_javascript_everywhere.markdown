---
layout: post
title:      "JavaScript, JavaScript Everywhere!"
date:       2019-02-15 19:37:33 +0000
permalink:  javascript_javascript_everywhere
---


Sometimes I think it’s important to go back over the basics and always remember a language’s foundation. So, I thought I’d review JavaScript’s major concepts and create a reference guide for these ideas. Feel free to use this post as a study guide or a review as I will keep it quick and to the point. 

* Var/Let/Const- 
   * **Var**- declarations are globally scoped when a var variable is declared outside of a function or within a block (var variables are not block-scoped). A var variable is function scoped if declared inside a function, can be re-declared and updated (can call var greeter twice without an error). 
   * **Let** and **const** variables cannot be re-declared. They are both block scoped. They also will throw an error if they are declared after they are used in a function (they are still hoisted, but not initialized). You cannot declare a const variable without also assigning it (it cannot be updated). 

* Scope 
   * **Variable scope**- the scope of a variable is controlled by the location of the variable declaration, and defines the part of the program where a particular variable is accessible. 
   * **Global scope**- any variable declared outside of a function belongs to the global scope and is therefore accessible from anywhere in your code 
   *	**Local scope**- each function has its own scope, and any variable declared within that function is only accessible from that function and any nested functions (function scope) 
   
*	**Hoisting**- all variable declarations are moved to the top of their cope (global or local), called hoisting as the variable declarations are hoisted to the top of the scope. Note that hoisting only moves the declaration, any assignments are left in place.
* **Callback function**- a function that is to be executed after another function has finished executing 
   * Callbacks are a way to make sure certain code doesn’t execute until other code has already finished execution 
*	**Closures**- can specify a callback by calling a closure 
   *	A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time. 
   *	To use a closure, simply define a function inside another function and expose it. To expose a function, return it or pass it to another function. 
   *	The inner function will have access to the variables in the outer function scope, even after the outer function has returned. 
   *	Closures are commonly used to give objects data privacy 
*	**This**- in most cases, the value of this is determined by how a function is called
   *	In the global execution context (outside of any function), this refers to the global object
*	**New** -creates a new object (type of this object is simply object)
   *	It sets this new object’s internal, inaccessible [[prototype]] (ie. _proto_) property to be the constructor function’s external, accessible, prototype object 
   *	It makes the ‘this’ variable point to the newly created object
   *	It executes the constructor function, using the newly created object whenever this is mentioned 
   *	It returns the newly created object, unless the constructor function returns a non-null object reference. In this case, that object reference is returned instead. 
*	**Context Binding** (call, apply, bind)- all three are used to control the invocation context of a function – call() and apply() allow you to specify the context (“this”) and immediately invoke the function with that value. The difference between the two is that apply() only takes two argument, the value you want to pass for “this” and an array of arguments to pass to the function. bind() returns a context-bound version of the original function.
*	Apply, call, bind 
   *	**bind()** returns a bound function that, when executed later, will have the correct context (“this”) for calling the original function. So bind() can be used when the function needs to be called later in certain events when it’s useful. 
   *	call()/apply() – used to invoke the function immediately 
       *	**call()**- runs the function in the context of the first argument and subsequent arguments are passed in to the function to work with (limitations become apparently when you want to write code that doesn’t or shouldn’t know the number of arguments that functions need) 
       *	**apply()**- the second argument needs to be an array which is unpacked into arguments that are passed to the called function 
*	**Equality Operator**- there are two types (== and ===), === is strict comparison and only true if the values are the same type and the contents match (type conversion). Type converting comparison == will convert the values to the same type before comparing (so “1” and 1 sould be == but not ===). 

*	**Arrow Functions**- introduced in ES6 – shorter syntax for defining functions and these functions do not have their own this, arguments or super – cannot be used for constructor functions. 
   *	Syntax: const funcName = ( ) => statement 
   *	They implicitly return statement if you don’t include {} block
   
*	**Spread Operator**- syntax … - can be used in function arguments or with array literals or objects. Purpose is to expand an array or object in places where zero or more arguments/elements are expected 
   *	Example: 
   
   `const array = [1, 2];`
	 
   `const array2 = [...array, 3, 4];`
	 
   `console.log(array2) // [1, 2, 3, 4]`

*	**Prototypes & Inheritance**- all JS objects inherit properties and methods from a prototype. 
   *	The Object.prototype is on the top of the prototype inheritance chain 
   *	This prototype property is an object (called as prototype object) has a constructor property by default. Constructor property points back to the function on which prototype object is a property. functionName.prototype 
   *	Prototype object of the constructor function is shared among all the objects created using the constructor function 
   
*	**Asynchronous JS**- control timing protocol in which a specific operation begins upon receipt of an indication (signal) that the preceding operation has been completed
   *	**Promises**- a promise represents the eventual result of an asynchronous operation. It is a placeholder into which the successful result value or reason for failure will materialize 
* **Higher Order Functions**- functions that operate on other functions, either by taking them as arguments or by returning them. In simple words, a Higher Order function is a function that receives a function as an argument or returns the function as output. 
   *	For example, Array.prototype.map, Array.prototype.filter and Array.prototype.reduce are some of the Higher-Order functions built into the language 
   
*	**Execution context**- the environment (or scope) in which the line is being executed 

*	**Event Delegation** refers to the process of event propagation (bubbling) to handle events at a higher level in the DOM than the element on which the event originated. It allows us to attach a single event listener for elements that exist now or in the future. 
    *	Mechanism of responding to UI-events via a single common parent rather than each child, through the magic of event “bubbling” (aka event propagation) 
*	Event bubbling and capturing are two ways of event propagation in the HTML DOM API, when an event occurs in an element inside another element, and both elements have registered a handle for that event. The event propagation mode determines in which order the elements receive the event. (Event propagation is a way to describe the “stack” of events that are fired in a web browser.) 
   *	With **bubbling**, the event is first captured and handled by the innermost element and then propagated to outer elements. 
    *	With **capturing**, the event is first captured by the outermost element and propagated to the inner elements. Capturing is also called “trickling” which helps remember the propagation order. 
*	**REST** (Representational State Transfer)- an architectural style for developing web services, is popular due to its simplicity and the fact that it builds upon existing systems and features of the internet’s HTTP in order to achieve its objectives, as opposed to creating new standards, frameworks, and technologies (HTTP Verbs: GET, POST, PUT, DELETE)
 
*	**Functional programming**- a form of programming in which you can pass functions as parameters to other functions and also return them as values. We think and code in terms of functions 

*	**Currying**- a way of constructing functions that allows partial application of a function’s arguments. You can pass all of the arguments a function is expecting and get the result or pass a subset of those arguments and get a function back that’s waiting for the rest of the arguments. 

 ![https://i.imgur.com/b4PAmAp.png](https://i.imgur.com/b4PAmAp.png)
 
 ![https://i.imgur.com/NVWGheg.png](https://i.imgur.com/NVWGheg.png)
 

These concepts are just some of the basics and there are plenty of other major ideas to understand, but hopefully this will act as a good summary for those of you trying to understand all of the main JavaScript concepts. 

![https://i.imgur.com/abBbaHV.jpg](https://i.imgur.com/abBbaHV.jpg)
 

