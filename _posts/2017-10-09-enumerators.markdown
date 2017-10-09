---
layout: post
title:      "Enumerators"
date:       2017-10-09 15:48:47 -0400
permalink:  enumerators
---


An **Enumerator** is a class which allows both internal and external iteration. 
Most methods have two forms: a block form where the contents are evaluated for each item in the enumeration, and a non-block form which returns a new Enumerator wrapping the iteration. 

In other words, such cool tools to master! 
I'm going to break down the basic ones that I've been using recently. 

# Boolean Enumerators:

**#all?** - the block passed to it must return true for every iteration

![](https://i.imgur.com/8RNb8Ju.png)
 
 
**#none?** – the block returns false for every iteration 

![](https://i.imgur.com/t9NU2Vk.png)
 
**#any?** – will return true if at least one iteration of the block evaluates to true, but false if none of them do.
![](https://i.imgur.com/7VUarxb.png)
 
**#include?** – will return true if the given object exists in the element. If it doesn’t find a match, it will return false. 
![](https://i.imgur.com/v9IfbaM.png)
 
# Search Enumerators:
**#select** - return value will be a new array containing all the elements of the collection that cause the block passed to #select to return true

![](https://i.imgur.com/5qhcSRk.png)
 
**#detect or #find** - only return first element that makes block true

![](https://i.imgur.com/OclcbK7.png)
 
**#reject** - return an array with the elements for which the block is false 

 ![](https://i.imgur.com/jnydQey.png)

**#sort** – yields to a block with two elements, that block is the comparator

The <=> symbol is called the combined comparison operator.

-	Returns 0 if first operand equals the second
-	Returns -1 if the first operand is less than the second
-	Returns 1 if first operand is greater than the second 

To kind of break down what the #sort method does, it looks like this in its full glory:

![](https://i.imgur.com/BKENR7F.png)

Which can be condensed into this: 

![](https://i.imgur.com/dOeP0i7.png)


So hopefully that gives you a quick understanding of how all of those enumerators work. They're a pretty powerful tool to use in your code which makes it important to really grasp these concepts. 

For more info on Enumerators:
[https://docs.ruby-lang.org/en/2.0.0/Enumerable.html](https://docs.ruby-lang.org/en/2.0.0/Enumerable.html)

