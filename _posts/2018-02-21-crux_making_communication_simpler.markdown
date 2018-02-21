---
layout: post
title:      "Crux: Making Communication Simpler"
date:       2018-02-21 18:21:15 +0000
permalink:  crux_making_communication_simpler
---



Communication. 

Its importance can never really be overstated. 
It always seems like a simple thing, but somehow it seems that every organization gets bogged down with overcomplicating communication. Many organizations get overwhelmed by email chains, extensive meetings, and misunderstood goals. 

With these issues in mind, I created “Crux”- a project management application that streamlines your company’s communication onto one platform. It ensures that the entire team is on the same page about what projects you’re working on, what tasks need to be completed for each project, and allows team members to communicate about the projects without getting confused with email chains. Everyone knows what’s going on and what they need to do. Simple. Finally. 


**The Process**

Planning out Crux took some time, but mostly it was narrowing down which aspects of the project I wanted to focus on first. I had so many ideas so deciding on the layout was a challenge. 
I eventually determined to create it as follows: 

Home page where users sign up or sign in

Once signed in, users have their Projects home page which displays all the projects the team is working on. From there, they can select a Project.

* Each project has a description and a tag (to determine which department is assigned to that project, i.e. Marketing, Development, Human Resources, etc.)
* Project Messages- where team members can discuss all project related items. 
* Project Tasks- what specific actions still need to be completed for this project
   *	When users go to “All Tasks” for a project, they can see all of the project’s tasks specified by which tasks are active and which are already completed. 

![https://i.imgur.com/FAODyHN.png?1](https://i.imgur.com/FAODyHN.png?1)   ![https://i.imgur.com/LOh3cXb.png?1](https://i.imgur.com/LOh3cXb.png?1)  ![https://i.imgur.com/NuKR183.png?2](https://i.imgur.com/NuKR183.png?2)

**Associations:**

I think associations is where I spent most of my time when I was planning out Crux.  Making sure the foundation was sturdy before moving forward seemed pretty darn essential. For nested resources like the projects’ messages and tasks, I associated them in the database with foreign keys (project_id), and for the project tags association, I used a join table (:project_tags). Once I had decided on the proper associations, the models were pretty simple, using belongs_to, has_many, and has_many through. 

I added validations to my models to ensure correct data, added a custom attribute writer, scoped methods for active and completed tasks, used Devise for user authentication (which came with a number of other complications in making sure all of my naming conventions were correct), and added Omniauth so that users could sign up or in through Facebook, along with a number of other fun aspects to my project. 


**Summary:**

Overall, I learned a lot from building Crux. I went through all of the ups and downs of programming something new: overwhelming excitement about my idea, frustration when I started running into walls, triumph when I figured out why an error occurred, feeling drained after countless errors and scouring the internet for answers that are often outdated or not helpful for my situation, followed by a moment of realization and exhilaration after figuring out my issues. 

I think the biggest piece of advice I have for other programmers facing something like this is: be patient with yourself and with your program. Plan out what you’re going to do and then focus on just getting one aspect working then another and then another. By narrowing down your focus to the building blocks, you won’t be overwhelmed by fixing everything at once. 


**Future Plans: **

I genuinely want to keep working on Crux in the future as a passion project. Additional features I’d like to add are: 

* Project Calendars so everyone is aware of project deadlines, events, and meetings. 
* User Check-ins so that we can see where each team member is at within their project
* Admin roles for more control over editing and deleting items 
* A more robust user profile with all assigned tasks listed and all user check ins to get a full summary of each team member 
* A killer layout with additional JavaScript and CSS 


How I feel finishing my project: 

![https://i.imgur.com/GV7ryw9.jpg?1](https://i.imgur.com/GV7ryw9.jpg?1)
 

