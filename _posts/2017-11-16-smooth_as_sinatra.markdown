---
layout: post
title:      "Smooth as Sinatra"
date:       2017-11-16 17:54:59 +0000
permalink:  smooth_as_sinatra
---


Lately I’ve been trying my hand at writing Sinatra and some basic web applications. While it was frustrating in the beginning, I’ve really been having fun with it! Honestly, I think once you can understand the big picture and how things are all related, it makes writing the code significantly easier. So, let’s go through it and make it easier for anyone else starting out with Sinatra! 

**Sinatra** is a domain specific language implemented in Ruby that’s used for writing web applications and is Rack based.  
* It has pre-written methods that we can include in our apps to turn them into Ruby web applications. 
* It’s designed to be lightweight and flexible, and has the bare minimum requirements and abstractions for building simple and dynamic Ruby web applications. 
* Use it by typing ‘Gem install Sinatra’ or ‘bundle install’

**Model-View-Controller**
The structure of web applications is fairly straight forward and separated into: controllers, models, and views. An analogy to help you understand is going to a restaurant. You order food (similar to a user/browser), the waiter (the controller) takes that order to the chef (the application’s database) and gets what the user asked for. The waiter then returns the order back to the customer’s table (the view and what the user ends up seeing). 

Models: Databases (the Chef) 
* Creating Data 		Song.create(:title => “Crazy”) 
* Retrieving Data		@song = Song.find(1) 
* Updating Data		@song.save 
* Deleting Data		@song.destroy

Controllers: Business Logic (waiters) 

Views: Display Logic (table) 


**A Sinatra Request 
Request Cycle** 
1.	Client makes HTTP request. Sinatra grabs it and routes it to the correct action. 
2.	Action asks model for objects 
3.	Model asks for the data 
4.	Database response 
5.	Model sends objects to action 
6.	Action sends objects to view for rendering 
7.	View responds with HTML 
8.	Controller sends back HTML in HTTP response 

![https://i.imgur.com/kRePH8x.png?1](https://i.imgur.com/kRePH8x.png?1)
# File Structure
**Database:**
Setting up your database for a web application is essential so that you can store all of your application’s information. Active Record has been an excellent resource to use for this endeavor. 

**ActiveRecord**
Like the dynamic ORM we built, ActiveRecord maps database tables to Ruby classes. 
* It’s a Ruby gem, meaning we get an entire library of code just by running gem install activerecord or by including it in our Gemfile. 
* You connect to a database and create tables
* ActiveRecord includes CRUD methods (Create, Read, Update, and Delete).  

**Migrations**- convenient way for you to alter your database in a structured and organized manner, allow you to describe these transformations using Ruby. 
-	Version control for your database
-	Connect to a database, create table using SQL or ActiveRecord::Migration config/environment.rb 
-	`Rake db:create_migration NAME=create_table` will create a migration for you automatically
-	Once you insert the data you would like in your database, run ‘rake db:migrate’
-	`Rake-T` shows the commands available with migrations
-	`Rake db:rollback` deletes your last migration. (It’s particularly useful if you make a mistake and need to take out your last migration.)
-	Methods up and down are like do and undo, but the change method is more common for basic migrations. 

 ![https://i.imgur.com/9SMhXQd.png](https://i.imgur.com/9SMhXQd.png)

**Models:**

Models are what tells your application how all of your data is related/associated to each other. Luckily with ActiveRecord, we can create these associations simply with `has_many` and `belongs_to`. But remember, if you say that one model `has_many` of another model, you need to also create a `belongs_to` association with that other model or your database will not remember the association. So, for example, if you’re creating Twitter, you would need to create a User model and a Tweets model. The user would `have_many :tweets` and the tweets would `belong_to :user`.
Example: 

 ![https://i.imgur.com/O5fWrpC.png](https://i.imgur.com/O5fWrpC.png)

**Controller:**
-	App.rb file or your app folder is the heart and soul of a Sinatra app
-	Our application controller- handles all incoming requests to our app & sends back the appropriate responses to the client.
* First line of app.rb is just requiring Sinatra gem so that we can incorporate its functionality.
* 	Next line, we define a class App and have it inherit from Sinatra::Base (so our App will have all the functionality of the Sinatra database).
* 	Controllers define an HTTP method using the Sinatra routing DSL provided by methods like GET and POST, when enclosed with a ruby class that is a Sinatra controller, these HTTP routes are scoped and attached to the controller.


-	**Config.ru-** purpose is to detail the Rack the environment requirements of the application and start the application. 
o	Config.ru requires a valid Sinatra Controller to run- a ruby class that inherits from Sinatra::Base, this inheritance transforms into a web application by giving it a Rack-compatible interface behind the scenes via the Sinatra framework. 
o	Final step is mounting it in config.ru -> mounting a controller means telling Rack that part of your web application is defined within the following class, we do this in config.ru by using `run Application` (or use `UsersController`) where run is the mounting method and Application is the controller class that inherits from Sinatra::Base and is defined in a previously required file 


**Routes**- the part of an application that connect HTTP requests to a specific method in your application code built to handle responding to such a request (that part of code is called a Controller Action) 
-	Our application gets a request from browser/URL/URI, the matching route defined in the controller would look like this: get ‘/’ do 
-	Once the request has been matched to the route in the controller, called the controller action then it executes the code inside of the controller actions block. 

A route is an HTTP method paired with a URL-matching pattern, each route is associated with a block: 

* 	Get ‘/’ do: show something 
* 	Post ‘/’ do: create something 
* 	Put ‘/’ do: replace something 
* 	Patch ‘/’ do: modify something 
* 	Delete ‘/’ do: destroy something 
* 	Options ‘/’ do: appease something 
* 	Link ‘/’ do: affiliate something 
* 	Unlink ‘/’ do: separate something 

![https://i.imgur.com/KVJWvZE.png1](https://i.imgur.com/KVJWvZE.png1)
 
**Return Values-** the return value of a route block determines at least the response body passed on to the HTTP client or at least the next middleware in the Rack Stack. Most commonly a string but other values accepted.
-	You can return any object that would either be a valid Rack response, Rack body object or HTTP status code. 


Example: 
 
 ![https://i.imgur.com/0W1fgJf.png1](https://i.imgur.com/0W1fgJf.png1)
 
(An awesome resource to use on this: http://www.sinatrarb.com/intro.html#Routes)


**Views: **

**Embedding Ruby (erb)**
-	Erb and other templating engines allow us to modify the content and structure of our HTML code. With erb, we do this using two different types of tags: the substitution tag (<%=) and the scripting tag (<%) 
* Substitution tag (<%=)- evaluates Ruby code and then displays the results into the view, inside tags you can write any valid Ruby code that you want. We use sub tags when we want to display some evaluation on the page, and we can wrap them in any other HTML tags we like.
* Scripting tag (<%)- they evaluate but don’t actually display Ruby code (often used with iteration and lists of items). 

-**	Layout.erb**- we need to add a yield wherever we want the other page content to be loaded ‘<%= yield %>’ (get layout.erb loaded around the index.erb) 
o	When controller action triggered (get ‘/’ do erb :index) and the erb method is called, it looks to see if there is a view titled layout.erb. If that file exists, it loads that content around the desired erb file. 

-	**Sinatra Nested Forms**- erb provides similar syntax as hashes, it handles that first level of nesting so instead of having to do my_hash[“student”] = { } we can go straight into the student hash.  
Erb assumes that the name of your top-level hash is the first key so the code to call the value associated with the nested “name” key would be student[“name”] 
The params hash is a “rack” object that is accessible through Sinatra’s request object. This params hash stores information posted by html forms in form of a hash which contains key-value pair. 

-**	Understanding Params: **
1.	Realize that because the params hash stores form data, the user’s entry should always be the value of a key-value pair. 
2.	If you think of params hash as having a pointer to what will be returned then every time you add on an extra layer, the data type of the extra layer- be it array or hash, will be the return of the formerly lowest layer. 
a.	Must end it with a key-value pair like <input name= “game[][name][][syllables]”/> 
3.	By convention, you leave the top-layer of the params hash as being without square brackets, despite that it is a key-value pair inside params hash. 
4.	When in doubt practice using this method in irb: require ‘rack’  def p(params) Rack::Utils_parse_nested_query(params) 

Example: 

 ![https://i.imgur.com/vj1jRJk.png](https://i.imgur.com/vj1jRJk.png)

If you’ve gotten this far, congrats! I know that it’s a lot to take in so give yourself some time. When I first learned ActiveRecord, I was astonished that I no longer had to do the tedious work of building ORM methods. With Sinatra, it took me a little bit of practice to really feel confident in implementing it on my own. Keep going though. I promise that once it clicks, you’ll have such a fun time creating new applications! 

