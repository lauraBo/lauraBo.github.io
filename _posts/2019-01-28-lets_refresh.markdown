---
layout: post
title:      "Let's Refresh"
date:       2019-01-28 11:19:08 -0500
permalink:  lets_refresh
---


The first time I read the Rails and JS project requirements, it immediately became clear to me that I needed to turn around and go straight back to the beginning of the JS section and go through it all once again. I grew painfully aware that I did not have the level of understanding needed to even attempt the project. In fact, there were some labs in the section that I went over three times to make sure that I had really grasped all of them. I also read a couple of books - 'Headfirst Javascript Programming' &  'A Smarter Way to Learn Javascript' ( a visual approach) so I could learn more about the foundation of what JS is and why it is used. When I had gone through through the JS section the first time round, I hadn’t achieved this level of understanding. I felt demotivated because my progress was somewhat slower than on previous sections. Once I had read the book and gone over the JS section a couple of times more, I then re-watched the four videos in the section ‘Using Ajax and Rails’. It was only after this thorough preparation and re-read the project requirements again that I felt confident enough to make a start.

It helped to think of incorporating JS into my Rails application into three steps:

1.HIJACK LINK
2.SEND A GET/POST REQUEST
3.RECEIVE RESPONSE & DISPLAY DATA 

I wanted to discuss three of the problems I came across while completing the project. 

* My associated data (stockists) wouldn’t display on the ‘Bourbon view’ show page.
* The javascript for the entire application only worked when I refreshed the page I was visiting.
* My ‘New Stockist’ form would not clear its fields on submit. 

**Tackling Problems**

1. I created a ‘Next’ button on the ‘Bourbon view’ show page and managed to successfully display the corresponding data for each bourbon though javascript. However, I couldn’t work out why the stockists that were associated to the individual bourbons were not being displayed. 

The original code:
![](https://imgur.com/lMWR6nH.png)



I tried a number of things. 

Firstly, I tried the obvious:

	$(".bourbonStockistName").text(data[“stockists”];

and then….


	$(".bourbonStockistName").text(data[“stockists”][“name”];

But neither of these worked. 

I did some research online about how to display associated ‘has_many’ data. I wondered if it had anything to do with my serializers, so I re-read the serializer section. I concluded that my serializer wasn’t causing the issue as it included the ‘has_many’ relationship and should have been displaying in the page:

	class BourbonSerializer < ActiveModel::Serializer
  		attributes :id, :name, :age, :grain, :description
  		belongs_to :distillery
  		has_many :stockists
	end

I visited the json URL endpoint to check what data I was getting back from the AJAX request: 

![](https://imgur.com/3sWYShe.png)



I could see that I had successfully completed the first two and a half steps - HIJACK, SEND GET REQUEST, RECEIVE DATA BACK …. 

The problem was clearly in the code that would display the data to the DOM. 
I had successfully displayed the associated distillery name, so why wouldn’t the associated stockists display? 

As it turned out, I  had not been looking at the json data correctly. The stockists data was an **ARRAY**. I couldn’t simply use the same code that I used for the distillery data to display:

 $(“.distilleryName").text(data["distillery"]["name"]);


I had to create a loop that iterated through each piece of data in the array:
![](https://imgur.com/RtMnZJ8.png)


I can’t tell you how happy I was to finally see the beautiful stockists data on the page!


2. It came as a nasty surprise to find that the dynamic features I had added to the app only worked, when I refreshed the page I was visiting. This defeats the purpose of using Javascript in the first place!

To overcome this, I removed two gems from the Gemfile:

gem 'jquery-turbolinks'
 gem 'turbolinks', '~> 5’

I also removed them from the manifest file. 

I had read that turbo links can sometimes affect the ‘document ready’ function inside your J.S files. Removing the two gems solved the loading javascript problem (without refreshing page) but unfortunately it also caused my javascript features on the Stockists index view page to stop working. After researching some possible solutions on SlackOverflow, I decided to re-install the turbo links gem, and add it to the manifest file again. Finally, I added the following line of code ‘turbolinks:load’ to the ‘document ready’ function in the stockists.js file:

![](https://imgur.com/QPnkzjp.png)


This solved the problem!


3. Clearing a form after  submit was not a requirement of the project, but I wanted to make the user experience better by clearing the text box afterwards. 
In one of the videos in the Ajax section, this was achieved by giving the textbox a blank value at the end of the submit form function. I tried this and it did not work for me for some reason.

Upon further research I found the ‘reset’ method. Unfortunately, this still didn’t work for me……… until I realised that I had been using the wrong ID. The ID I should have been using was #new_stockist and not #stockist-form. Using the inspect tool in the chrome browser, I could see that the form id was #new_stockist. I was trying to reset a div container with the ID #stockist-form.  The code that finally got the form to submit: 

$("#new_stockist")[0].reset();


It was proved to me yet again how useful the projects are at the end of each segment. They made me aware that I didn’t have the understanding I needed and forced me to go back and review. It also highlighted my personal need for supplementary reading alongside the online learning. I have to admit that javascript has been the most difficult and challenging section yet. There were times I just couldn’t understand why none of the material was clicking! I began to tell myself that it was ok that I didn’t get it. I was genuinely worried that I would never be able to start the project as I had so little confidence in my abilities to even attempt it. Not only do I feel a great sense of relief at getting through it, but a real sense of achievement too. Perhaps I would go so far as to say that this has been the most fulfilling project to date! 
