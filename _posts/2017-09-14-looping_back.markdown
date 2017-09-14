---
layout: post
title:  "Looping Back"
date:   2017-09-14 00:28:14 +0000
---


Iteration pretty much blew my mind. Enough that learning these concepts made me wonder if my mind was even still there afterwards. My initial relationship with Procedural Ruby was frustrating, to say the least. After reading through all the material, completing the labs, taking notes, and reviewing everything, I finally really appreciate everything that iteration can do. From what I can tell though, it’s a common topic to get confused on. So for anyone out there still struggling through it, I’ve collected my favorite notes from my lessons at Flatiron School and a few online articles to help you understand these concepts! 


![](https://i.imgur.com/jAOHCDJ.jpg)      ![](https://i.imgur.com/0Kq33ye.jpg?2)
                                                     Actual photo of me studying this material.
									
									
									

**Iteration and Abstraction**

*Looping-* occurs when you tell your program to do something a certain number of times.
* Loop do- every step is accounted for explicitly in the code.
* While loop- initializing a cycle of behavior based upon a condition.

*Iteration-* occurs when you have a collection of data (for example, an array), and you operate on each member of that collection.
* #each – a block is passed to #each, opened by the code that starts with do and closed by end. The block passed to each is executed once for each element in the original collection. 

* We call each run, each execution, of the block passed to the iterator (#each in this case), an iteration. It's a word used to refer to each 'step', or each 'execution', of a block. An iteration is the singular execution of a sequence of code (that we call a block) within a loop.

* When we iterate over a collection of elements using #each (and also in other iterators and enumerables), the iterator #each yields each element one at a time to every iteration via a variable declared with the opening of the block.


Ex: If I tell my program to print out the phrase "I love programming!" five times, that's looping. If I tell my program to enumerate over the array [1, 2, 3, 4, 5] and add 10 to each number, that's iteration.

The goal of *abstraction* is to remove details. It makes our code “absolutely precise." We are able to express ourselves as clearly and honestly as possible. 



**A block-** a bit of code enclosed in do/end or curly brackets { }.

It can be:
1. Multi-line between do and end
2. Inline between { and } 

![](https://i.imgur.com/tDwVXdG.png) 

The n is called a **block parameter**- the value in this case is each number in turn.
The variable name inside the “pipes” acts as an argument that is being passed into the block. 


* Each method yielding each element of array to block, code in block is executed, using each successive element from the array as the iteration proceeds 
* #each, #collect rely on the yield keyword



**Yield-** when used inside the body of a method, it allow you to call that method with a block of code and pass or yield to that block (“stop executing the code in this method and instead execute the code in this block then return to code in method”).

![](https://i.imgur.com/u187jzM.png)

**Passing Blocks to Methods:**
* A method doesn’t need to specify the block in its signature in order to receive a block parameter. You can just pass a block to any function, but unless that function calls yield, the block won’t get executed. 
* If you call yield in your method then the block parameter becomes mandatory and methods will raise an exception if it doesn’t receive a block.
* Use block_given? to make the block an optional parameter. 

*You can call yield with arguments:*
* Any parameter passed to yield will serve as a parameter to the block.
* The parameters inside the block are local to the block (unlike those passed from method to the block).


![](https://i.imgur.com/RvmxO17.png)

**&block-** pass a reference to the block (instead of a local variable)
* Ruby allows you to pass any object to a method as if it were a block.
* If it’s already a block, it will use the passed in object, but if it’s not a block, it will call to_proc on it in an attempt to convert it to a block. 
* Call on the block is the same thing as using yield (block.call).


**Block, Proc, Lambda?**
* Blocks are a chunk of code and yield allows you to inject that code at some place into a method. You can have one method work in different ways, you don’t have to write multiple methods (you can reuse one method to do different things). A block is a Proc.
* The only difference between a block and a proc is that a block is a Proc that cannot be saved and is a one-time use solution. 
* Lambdas act just like methods, as they check the number of arguments and do not override the calling methods return. It’s best to think of lambdas as another way to write methods, an anonymous way at that. 

**When to Use a Block, Proc, or Lambda:**
1. Block: Your method is breaking an object down into smaller pieces and you want to let your users interact with these pieces.
2. Block: You want to run multiple expressions atomically, like a database migration.
3. Proc: You want to reuse a block of code multiple times.
4. Proc: Your method will have one or more callbacks.
5. Use lambdas if sending a method to another method that can return a method.



During one of my study sessions, Corinna gave us this handy dandy Iterator Cheatsheet on Iterators that might help you out: 

![](https://i.imgur.com/GEMJ8mu.png?1)


And lastly, some resources you can go to and get further explanation: 
* [https://mixandgo.com/blog/mastering-ruby-blocks-in-less-than-5-minutes](https://mixandgo.com/blog/mastering-ruby-blocks-in-less-than-5-minutes)
* [http://www.reactive.io/tips/2008/12/21/understanding-ruby-blocks-procs-and-lambdas](http://www.reactive.io/tips/2008/12/21/understanding-ruby-blocks-procs-and-lambdas)
* [https://allaboutruby.wordpress.com/2006/01/20/ruby-blocks-101/](https://allaboutruby.wordpress.com/2006/01/20/ruby-blocks-101/)






