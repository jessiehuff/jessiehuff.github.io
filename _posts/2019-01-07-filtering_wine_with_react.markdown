---
layout: post
title:      "Filtering Wine with React"
date:       2019-01-07 18:11:49 +0000
permalink:  filtering_wine_with_react
---


I was recently working on a React project for a really awesome company, and there were a lot of fun features in the project that made me want to discuss it. The project itself was a wine list that pulled in data from an API, and I had to create a “select year” feature that would have a drop-down list of all the wine years available. When a year was selected from the list, it showed the wines available from that year. 

So, I thought that this would be a perfect job for state! I could make the selected year from the drop-down menu a part of the wines page state and create some logic for filtering the list of available wines based on that selected year to conditionally render the page. 

I constructed the state in the Wines component like so:

![https://i.imgur.com/NUmZ4pF.png](https://i.imgur.com/NUmZ4pF.png)
 
In my event handlers, I have one called sortWines for setting the state to the year selected and one called goBack that resets the state to an empty string if the user wants to go back to the full list. 
 
 ![https://i.imgur.com/BKbBZZf.png](https://i.imgur.com/BKbBZZf.png)

In terms of logic, I wanted to make sure I organized the years for the dropdown menu. In order to do this, I took all of the wines (in the below example, allWines is set to `this.props.wines’) and mapped it based on the year. Then I created some code that would ensure that it would only show unique years. The native method filter will loop through the array and leave only those entries that pass (or get a true return value) the given callback anonymous function. The callback anonymous function returns true if the entry is the first occurrence and false elsewhere. It uses the native indexOf method which finds the index of the first occurrence of an entry in the array. I pass the array of all wine years through this and then chain on the sort() method that sorts the array alphabetically so the list shows in ascending order. 
 
 ![https://i.imgur.com/4MjdNg6.png](https://i.imgur.com/4MjdNg6.png)
 
Once I have the list showing the correct available years, I then focus on filtering the list of wines. I created an if/else statement so that if there is no selected wine or someone wants to return to the main list, the wineList used to render the page will just be the original props. However, if there is a selected year, the wineList used will be a filter of all wines in that year.
 
 ![https://i.imgur.com/awGkajx.png](https://i.imgur.com/awGkajx.png)
 
Inside the returned HTML, I have the dropdown menu mapping through the uniqueVintages (all unique years of the wine list) and adding the event handlers for both the scenarios in which they select a year or want to return to the full list. In the actual index of wines, I have it mapping specifically from the wineList that is either `this.props.wines` if no year is selected or a filtered list based on the year selected. This allows it to only render the list that we want. 

![https://i.imgur.com/z5aoDy8.png](https://i.imgur.com/z5aoDy8.png)
 
The finished product looks something like this: 
 
 ![https://i.imgur.com/IEOrIKz.png1](https://i.imgur.com/IEOrIKz.png1)

And once a year is selected, it filters the data accordingly: 

![https://i.imgur.com/q1flDBM.png1](https://i.imgur.com/q1flDBM.png1)
 

Cool, right? It was such a fun project to work on so I was super excited to get this feature working. Let me know if you have any questions! 


![https://i.imgur.com/mKew444.jpg](https://i.imgur.com/mKew444.jpg)

