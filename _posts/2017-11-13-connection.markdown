---
layout: post
title:      "Connection"
date:       2017-11-14 01:36:55 +0000
permalink:  connection
---

> “In an extreme view, the world can be seen as only connections, nothing else. We think of a dictionary as the repository of meaning, but it defines words only in terms of other words. I liked the idea that a piece of information is really defined only by what it’s related to, and how it’s related. There really is little else to meaning. 

> The structure is everything. There are billions of neurons in our brains, but what are neurons? Just cells. The brain has no knowledge until connections are made between neurons. All that we know, all that we are, comes from the way our neurons are connected.” 
> -Tim Berners-Lee

Connection. 

It is both who are and what we crave. It’s the very reason the internet was even created. The web was built not just to connect machines, but to connect people, like Tim Berners-Lee so eloquently explains. Even Google’s incredibly successful search algorithm is based on connection. PageRank measures the number of sites that link to a particular page and the words they use to describe those links. The idea is that the meaning of something is not present in the thing itself but rather in the way it connects to other things.

The web operates based on conversations between the client (the browser) and the server (the code running the website). 

![https://i.imgur.com/cbgwq6l.png?1](https://i.imgur.com/cbgwq6l.png?1)

Essentially it works like this (called the **Client Server Model**):
* Web page is a document 
* User inputs http://example.com
* The client (browser) makes a GET request 
* The server sends a response 
* The browser renders the page

Someone requests a web page through the URL/URI: 
Example: 
http://github.com/jessiehuff 
-	http - protocol 
-	github.com – domain
-	/jessiehuff – resource 


**Protocol** is the way we’re sending our request, and there are several different types of internet protocols (SMTP for emails, HTTP for secure requests, FTP for file transfers). 

The **domain** name is a string of characters that identifies the unique location of the web server that hosts that particular website. This is things like youtube.com and google.com. 

The **resource** is the particular part of the website we want to load. 
A good analogy is an apartment building. The domain is the entire building, and the resource is a specific apartment. 

Rendering broken down:
-	HTML – the Structure 
-	CSS – the Style 
-	Javascript – the Behavior 

**HTTP Verbs** 
(Used in server requests)
-	HEAD- asks for a response like a GET but without the body 
-	GET- retrieves a representation of a resource 
-	POST- submits data to be processed in the body of the request
-	PUT- uploads a representation of a resource in the body of the request 
-	DELETE- deletes a specific resource 
-	TRACE- echoes back the received request 
-	OPTIONS- returns the HTTP methods the server supports 
-	CONNECT- converts the request to a TCP/IP tunnel (generally for SSL) 
-	PATCH- apply for a partial modification of a resource 


Once your server receives the request, it will do some processing (run the code you wrote) and then send a response back. Server’s response is separated into two sections: headers and the body 

**Headers**- all the metadata about the response (content-length/how big is my response) and what type of content it is. Headers also include the status code of the response.

**Body** of the response is what you see rendered on the page. It is all of that HTML/CSS that you see.

![https://i.imgur.com/D2jJGEO.png](https://i.imgur.com/D2jJGEO.png)


The status code will then let us know whether the process was successful or if an error occurred. They are categorized as the following:  

**STATUS CODES**
-	100: informational (request received and continuing process) 
-	200: success (request successfully received, understood, and accepted) 
-	300: redirect (further action must be taken to complete request) 
-	400: error (request contains bad syntax and can’t be completed) 
-	500: server error (server couldn’t complete request) 



At the end of the day, this is what happens so that we can check our email, surf the web, watch YouTube videos, and messages our friends on Facebook. It’s the connecting force behind so much of our daily activity, and it’s essential for a developer to understand. 

Connection is the very reason that we developers exist. 

