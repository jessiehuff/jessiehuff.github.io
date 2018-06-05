---
layout: post
title:      "Varying Variables"
date:       2018-06-05 00:08:15 +0000
permalink:  varying_variables
---


After working with JavaScript for a while, understanding variables, scope, and hoisting seem to be key components in understanding any level of code. So, I’ve built out a quick reference guide for any of you still trying to master these concepts.

Of course, with anything in programming, you can always go deeper in each of these ideas, but I’ve laid out the basic outline. 

**Scope**- where the variables are available for use 

**Hoisting**- where the program pulls the specific variables and functions to the top level of code so that they’re loaded into memory during the compile phase


# **Differences in Variables**: 
•	**`var`**- the variable may or may not be reassigned, and the variable may or may not be used for an entire function, or just for the purpose of a block or loop
* **Var declarations** are globally scoped or function/locally scoped. 
     * It is *globally scoped* when a var variable is declared outside a function. This means that any variable that is declared with var outside a function block is available for use in the whole window. 
     * Var is *function scoped* when it is declared within a function. This means it’s available and can be accessed only within that function.
* **Hoisting**: var variables are hoisted to the top of its scope and initialized with a value of undefined 


•	**`let`** is a signal that the variable may be reassigned, such as a counter in a loop, or a value swap in an algorithm. It also signals that the variable will be used only in the block it’s defined in, which is not always the entire containing function.
* **Block scoped**- a block is chunk of code bounded by { }. A block lives in curly braces. Anything within curly braces is a block. So, a variable declared in a block with the let is only available for use within that block.  (let variables are block scoped) 
* Let** can be updated but not re-declared**- just like var, a variable declared with let can be updated within its scope. Unlike var, a let variable cannot be re-declared within its scope. (Both instances are treated as different variables since they have different scopes.) 
* **Hoisting**: let declarations are hoisted to the top. Unlike var which is initialized as undefined, the let keyword is not initialized. So if you try to use a let variable before declaration, you’ll get a Reference Error.


•	`const` is a signal that the identifier won’t be reassigned. Variables declared with the const maintain constant values. Const declarations share some similarities with let declarations. 
* Const declarations are **block scoped**- like let declarations, const declarations can only be accessed within the block it was declared. 
* Const **cannot be updated or re-declared**- this means that the value of a variable declared with const remains the same within its scope. It cannot be updated or re-declared. 
* Every const declaration **must be initialized at the time of declaration**. The properties of this objects can be updated. 
* 	**Hoisting**: like let, const declarations are hoisted to the top but are not initialized. 

# Functions and Hoisting: 
While variable names are hoisted and not defined, named functions has its entire function hoisted to the top and is accessible. Unnamed functions and function expressions do not get hoisted and so their variables are not accessible globally. 

So, for example: 

`function foo( ) { … } `

-	This entire function is hoisted and therefore accessible globally. 

`var foo = function( ) { … } `

-	This does not get hoisted and so the variables are not accessible globally. 

# Arrow Functions: 
Arrow functions were introduced with ES6 as a new syntax for writing JavaScript functions. They save developers time and simplify function scope. They are a more concise syntax for writing function expressions. 

-	An arrow function expression has a shorter syntax than a function expression and does not have its own this, arguments, super, or new.target. These function expressions are best suited for non-method functions, and they cannot be used as constructors.
     * 	Makes our code more concise and simplify function scoping and the `this` keyword. 
     * 	Reduces the confusion surrounding the `this` keyword- in code with multiple nested functions, it can be difficult to keep track of and remember to bind the correct this context. 
    



Resources for further information: 

https://dev.to/sarah_chima/var-let-and-const--whats-the-difference-69e

https://www.sitepoint.com/es6-arrow-functions-new-fat-concise-syntax-javascript/

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions

