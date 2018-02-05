---
layout: post
title:      "Fools Rush In? "
date:       2018-02-05 11:49:45 -0500
permalink:  fools_rush_in
---

They say that ‘fools rush in’, but they also say ‘the early bird catches the worm’. Which of these two proverbs is true? 
After my experience of doing this project, I would say that both are!

I was excited to get started on this project after watching Avi’s Daily-Deals video, in which he creates a data gem from scratch. So I got going by reading over the info on ruby gems.com and soon felt that I understood the basics. Without really thinking about the hows and whys, I almost immediately decided on the website from which  I was going to parse the information I needed from StoreForTheDogs.com - the online store for School for The Dogs . I spent some time after that thinking about how a user would interact with my code. I wanted my app to display a list of dog toys, and then offer the user the option to select one of them to subsequently receive further information about the product that they had selected as part of their purchasing user experience.

After typing ‘bundle gem’ into terminal, a framework for my gem was instantly created. It was both exciting and daunting seeing all those empty files ready for me. I started by setting up the bin file, and then I tested that it was working. This was simple enough. I then moved on to inserting the require statements needed in order to load my library of code. At this point, I have to admit I felt somewhat confused about what required what, and where I needed to require it! I then got an ‘unrecognised constant’ message so I went back to the Daily-Deal video to understand this area a bit more. Once I resolved those issues, I started work on defining my call and menu method.

It was whilst I was working on my scraper methods that I realised I had chosen an unsuitable website to scrape! I had wanted to scrape a website that contained all the names, prices and descriptions of the dog toy products all on one webpage. Unfortunately, when you are looking at dog toys on Store for the Dogs website, the website requires you to click on the photo or name of the product, which then links you to another web page containing the full description. I panicked! I felt that I had come too far with my idea to start from scratch with another website now.  However, I would only be able to scrape a single product with the gem I had now. 

As Avi says in the video “ the only way to progress is writing more code, discovering what my programme needs.” …..so I did the opposite. I was scared to tinker too much with what I already had created and write more code that would potentially make it over complicated or, at worst, unusable.  I left the application as it was. I didn’t feel I knew HOW to add to it and therefore left it as it was rather than try to work it on it. 

The next morning I woke up and made a video of how a user would interact with my gem. I didn’t feel proud of it.  It didn’t DO anything. I felt like i’d chickened out the night before and consequently felt embarrassed to submit the project. 

I then decided that I was going to start from scratch and this time I was going to prepare and plan like nobody’s business! I watched The Daily Deals video a further 4 times. I took notes. I read anything about Ruby Gems I could find on the net. I looked at other people’s gems on Github. I printed out the code for the Restaurants CLI, the Daily Deals gem and the Now Playing gem and studied all of them. I spent a day thinking about how I could make an app that would impress and use complex code that i’d be proud to submit. I spent ANOTHER  day thinking about what to do. I realised I felt daunted and overwhelmed again and was purposefully delaying starting. I eventually came to the decision that I would build a gem that scraped data from a pet adoption site. It would take in a zip code and then display the pets that were available in that zip code for adoption. After taking several steps back before I ran down that tunnel with my new idea, I decided to stick to my original plan as I was worried that it wouldn’t fulfil the spec for project of implementing both a list and details view. 

I ultimately realised that I was going to have to face my fears and go back to my original project and see how I could improve it. I’d wasted enough time as it was. I liked the index number method used in the restaurant cli gem to create a list of restaurant objects, but I had no idea how to implement that into both my scraper method for name and price, and the separate scraper method for description, as multiple web pages are involved. I decided that I would add another scraper method for one more toy, and then create an array to put the results of the scraper methods in. 

So what did I end up submitting after my circuitous journey? Well, my final gem can list only two products. If I could change anything about my gem, I would have created a method that accepted a URL and could scrape ALL the products and their respective descriptions on School for the Dogs website, regardless of whether they were on multiple pages or not. Perhaps I would need a function that can scrape from an array.


Am I proud of what my gem can DO? No, not really. 
Am I proud that I now know what a gem is and can name each of the components and describe what they do? Yes, I am actually! It feels really cool. And I still get that buzz when I type ‘bundle gem’ into terminal and see all those fresh files waiting for me to create something new!

Going through this journey, I have realised how keen I am to be able to develop my coding knowledge so to realise both my original vision of a gem that can scrape the full School for Dogs website AND my second idea of scanning dog adoption websites by zipcode. I am keen to learn more!

