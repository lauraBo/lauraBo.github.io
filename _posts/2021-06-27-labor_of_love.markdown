---
layout: post
title:      "LABOR OF LOVE"
date:       2021-06-28 03:07:01 +0000
permalink:  labor_of_love
---


To give you an idea of how long I’ve been attempting to do this project and how long I’ve been trying to grasp Javascript as a whole, I started this project when I was pregnant and my daughter is now two years old. 
 
I’m not going to lie - there have been many times where I have wanted to give up and accept that I might never understand the concepts in this project and finish building my app.  But I was determined to finish this project having spent so long on it, and I never ever gave up – because I desperately wanted to graduate from this course. I also wanted to be sure that I had done my best, and that all my efforts would not be in vain. I had done everything I could not only to complete the project, but to completely understand all the elements of the project - Javascript, React and Redux. 
 
 
The project requirements:
 
The code should be written in ES6 as much as possible
Use the create-react-app generator to start your project.
Your app should have one HTML page to render your react-redux application using 2 container components, 5 stateless components, and 3 routes.
The Application must make use of react-router and proper RESTful routing
Use Redux middleware to respond to and modify state change
Make use of async actions to send data to and receive data from a server
The Rails API should handle the data persistence and should be using fetch within your actions to GET and POST data from your API.
Your client-side application should handle the display of data with minimal data manipulation.
The application should have some minimal styling: feel free to stick to a framework (like react-bootstrap), but if you want to write (additional) CSS yourself, go for it!
 
Looking back now, when I first started the project in 2019, I wasn’t quite ready to do so - I didn’t have a full understanding of React & Redux but thought that maybe I could develop a fuller understanding as I built my app. I now realize that this belief was misguided - I grew more and more overwhelmed the more code I added. In fact, I was afraid to begin the front-end client-side part of the app, and so ended up spending a lot of time on the Rails side and ended up creating quite a very detailed back end of the app ( https://github.com/lauraBo/airbnbclone-rails-backend) I should mention here that I followed a code- along course (https://code4startup.com/projects/build-airbnb-with-ruby-on-rails-level-1) but tailored the code to my own needs. I thought that I could create the Rails backend and then move onto coding the client side. However, once it came to building the client folder I realized that I was in over my head. The code in the StartUp4code course I had followed was written for using rails as a standalone, not an API… and I had no idea which files to remove, move or edit, which view pages to delete or use, and ultimately which data I could or could not use.  At that stage, I was reluctant to give up on what I had already done as I had put so much time and effort into it already.  My original plan was to finish the project before I gave birth…. but that didn’t happen, as I felt very unwell throughout my pregnancy. Once my baby daughter came along.. well….I didn’t even have time to shower, much less code. What I did do was read up on React. I was so determined to grasp it! I found this book particularly helpful (https://www.amazon.com/Learning-React-Hands-Building-Applications/dp/013484355X) 
 
Ultimately, what helped me the most was re-doing the React and Redux section of the Flatiron course. This time around,  I took my time and only moved on once I felt I had completely grasped the objectives of each module. This meant only doing one or two lessons per day.  However, I knew that I had to be patient with myself. The extra time I put in to re-learn the concepts would serve me very well when it was time to restart the project. 
 
A New Start
And I did start again. With a completely new idea. This time, I wanted to start small and focus on fulfilling the requirements of the project first and foremost. If I wanted to add more afterwards, I could, but only after I had mastered the basics. I wanted to create something that I would use in my everyday life as I felt this would drive me forward and make the project less abstract for me. So I decided to create an app that would allow me to log recipes for my newborn baby daughter. The idea for this project grew out of a personal desire to have one central place where I could add the numerous recipes that had caught my eye when scrolling instagram, searching through cookbooks, looking through magazines or reading mom blogs.
Feeding my toddler is a huge challenge and I often find it stressful. Part of that is I feel a huge pressure to provide her with not only a variety of different food groups, but recipes that she will actually eat. I wanted a place I could come when I was looking for meal inspiration without having to think where I had ‘stored’ the recipes that I wanted to try for my daughter. I had turned corners of pages in books, took screenshots of the Instagram recipes and blog recipes but I just didn’t have the time to go scrolling through my photos folder or flip through a book trying to find the recipes. Hopefully this app is the solution to this and saves the busy parent time and mental energy! 
 
My User story:
Who is my User?  - Busy parents of babies and toddlers
What is their pain point?  Too many recipes, from multiple sources and no time to print/bookmark/ find them
How do they use my solution to overcome this problem? Saving recipes from multiple resources into one central API
 
To set up my React/Redux frontend and my Rails API, I followed the directions in this very helpful article:
https://dev.to/mmcclure11/how-to-setup-a-rails-api-and-react-js-client-3im3
 
I actually made two attempts to set up the project because I had forgotten to use create-react-app - one of the main requirements for the project. So, second time around, I set it up using the create-react-app command. 
 
Creating a new rails project was like greeting an old friend. Enjoyable, familiar and I didn’t have to work too hard!  I have been asking myself whether this means I am more cut out for backend programming rather than frontend!
 
Next step was to figure out how to connect the front end to the back end. I found the following online article very helpful: https://pamit.medium.com/todo-list-building-a-react-app-with-rails-api-7a3027907665
 
The article introduced me to Heroku which allowed me to run both Rails and React. Perhaps one of the most exciting parts of the process for me was moving the client folder into the API and seeing Heroku work its magic and open up localhost:4000! I remember thinking - I guess this means that my API and React are running at the same time? How exciting!
 
As you can imagine, creating my app from there on challenged me in many ways. Below I discuss a few of the noteworthy challenges I overcame and, in so doing, deepened my understanding of the concepts involved. 
 
I came across a CORS issue very early on and  it was whilst reading online in search for a solution that I found some very helpful advice that I used thereafter: Don’t just copy and paste any old code you find to try and fix a problem. Really understand the problem before you decide on which solution to use. I have certainly been guilty in the past of throwing whatever I can at something and crossing my fingers that it would work. With this in mind, I decided to look into what CORS was. 
 
‘Cross-Origin Resource Sharing (CORS) is an HTTP-header based mechanism that allows a server to indicate any other origin (domain, scheme, or port) than its own from which a browser should permit loading of resources.’
So this meant the issue lay inside the header and I found that I needed to make a very small tweak to my CORS file to fix the problem:
 
<a href="https://imgur.com/wUv4YLV"><img src="https://i.imgur.com/wUv4YLV.png" title="source: imgur.com" /></a>
 
This would enable the API to accept all cross origin requests. 
 
Having connected the backend to the frontend, I found myself feeling overwhelmed once again. Where do I go from here? I decided to start with React Router and work from there. I would decide upon my three routes and this would help give me an idea of what components I needed to create. I’m not sure this was the right place to start but going back to the router lab in the course as a guide certainly helped. On reflection, I could have done more upfront planning before starting the project - drawing a proper outline of each component and what they needed to import. It would be interesting to learn how fellow coders go about their planning for a react project with components. Where do they start? 
 
I decided to add Redux in at the last stage. Before attempting to integrate Redux, I would say that I was familiar with the vocabulary of Redux - reducers, store, state, action - but I did not understand it well.  This project, like all my previous projects, proves that I learn best by doing. For example, it wa sonly through doing that I understood that a Reducer is so named because it combines two pieces of information (current state and action) and then reduces this combination into one value. Doing helped to solidify my understanding that the reducer function never updates previous state, but rather creates a new state object.
 
Another challenge that I overcame involved ‘Hook calls’:
 
Error: Invalid hook call:
 
Hooks can only be called inside of the body of a function component. This could happen for one of the following reasons:
1. You might have mismatching versions of React and the renderer (such as React DOM)
2. You might be breaking the Rules of Hooks
3. You might have more than one copy of React in the same app
See https://reactjs.org/link/invalid-hook-call for tips about how to debug and fix this problem.
 
I looked into the first suggested reason and found that I didn’t have mismatching versions of React and I also ruled out having an extra copy of React.  I moved onto suggestion number two - breaking the Rules of Hooks.
 
What is a Hook?
Hooks are functions that let you “hook into” React state and lifecycle features from function components. They let you use React without classes. Hooks are JavaScript functions, but they have two additional rules:
 
From Reactjs.org:
Only call Hooks at the top level. Don’t call Hooks inside loops, conditions, or nested functions.
Only call Hooks from React function components. Don’t call Hooks from regular JavaScript functions. (There is just one other valid place to call Hooks — your own custom Hooks. We’ll learn about them in a moment.)
 
My console log suggested that I was probably breaking the Rules of Hooks in my App.js file so I wrapped the redux provider, store setup and reducer in a functional React component and it seemed to clear the issue. 
 
Redux Devtools 
I found the devtools extremely helpful when trying to find causes of errors.  I was struggling to render my recipes array and I began to wonder if my API was even connected to my client folder. The devtools enabled me to see that the array was being passed through but the problem was in the recipes component. I could have kicked myself as I had spent two full days on one particular error only to realise that I needed to removed ‘this’ from this.recipeList:
 
<a href="https://imgur.com/iCIuAbo"><img src="https://i.imgur.com/iCIuAbo.png" title="source: imgur.com" /></a>
 
That led me to again question the use of ‘this’ (I had found the concept difficult to grasp during my very first project back in 2017!) this time specifically in React. 
 
The following excerpt is from  https://medium.com/byte-sized-react/what-is-this-in-react-25c62c31480  - a great article by Trey Alexander Davis that helped me to understand the role of ‘this’ in React
‘The value of ‘this’ in JavaScript functions is determined by how a function is called. Methods like call, apply, and bind explicitly set the value of ‘this’ in a function, however if ‘this’ isn’t explicitly set, then ‘this’ will default to the global context.’
The issue may also have been due to the fact that the arrow function introduced in ES6 is a function with the current ‘this’ context already bound to the function. 
 
Although React's API has very few concepts to learn, I found them a challenge to grasp and put into practice. However, once I understood, I came to realize why it is so popular in the developer world and understand why one would use a component-centric approach for separating concerns. I also appreciated the create-react-app package, which allowed me to start development instantly. Furthermore, React minimizes DOM changes which means it is highly efficient for mobile apps in particular. It does this by monitoring the values of each component's state with the Virtual DOM. When a particular component's state changes, React compares the existing DOM state with what the new DOM should look like. From there, it decides upon the least ‘expensive’ way to update the DOM. Lots of clever stuff going on behind the scenes! 
 
I now want to use React to build a new user interface onto my previous projects like the Bourbon app I created for the Rails project. There is also lots of room to expand on my Toddler recipe project - the ability to edit and delete individual recipes would be very valuable addition.
 
I may have not built the most complex app, but it feels awesome to know that I built this from nothing. I feel good that my determination to get to grips with React and Redux led me to finally finish this project and this course and that feels really good!
I want to thank the kind, encouraging and inspiring tutors and friends that I met on the course. Because of you all, I kept going and you fostered a curiosity and love for learning code that remains to this day. I am excited to see where I can go from here. I am also excited to start my daughter coding at a young age! I wonder what her first app will be……
