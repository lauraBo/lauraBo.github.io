---
layout: post
title:      "BOURBON HUNTER"
date:       2018-08-24 23:30:02 -0400
permalink:  bourbon_hunter
---


Like the Sinatra project, for this Rails project I spent a large amount of time preparing in advance. Also like that last project, despite my extensive preplanning, I nonetheless hit numerous unexpected roadblocks along the way. This time though, it wasn’t my ignorance of GitHub that was to blame, it was my lack of understanding of the concept of a join table, amongst other things.

To start, I considered what kind of models I would need to fulfil the requirements of the project.  I originally came up with the following models:

**Models:  Agency, Agent, Actor
**
Agency has many Agents
Agency has many Actors through Agents
**
Agent has many Actors 
Agent belongs to an Agency

**Actor belongs to an Agent**

The join table would be the Agents’ table and the user submittable attribute would be **appointment_times **

I was very glad that I double-checked my ideas with my section leader before I went any further with the project. Luisa quickly informed me that these models would not fulfil the project requirements. She explained to me that, while  I had got the types of relationships and the user submittable attribute, by definition, “a join table is the "go-between” specifically in a many-to-many relationship.” Consequently, in my example, an agency has many users through agents, but a user doesn’t have many agencies through agents. She explained further: “It has to go both ways. To put it another way, you’ll be looking at least two belongs_to relationships on a join model.”

So…with a many-to-many relationship you can link two tables together, but in some situations you may also need to store other information about the many-to-many relationship. In those situations, you have to create a third table- the join table. The join table is where you can store attributes of the relationships between the two models. (https://support.airtable.com/hc/en-us/articles/218734758-A-beginner-s-guide-to-many-to-many-relationships) 

I decided to move away from the acting agency idea and restart with an entirely different concept. Having recently moved to Louisville, I wanted to create an app that had some affiliation with the local area ( and move away from anything dog-related..my last two projects were about dogs). I decided to create a content management system for Kentucky Bourbon. I can feel myself becoming more of a bourbon connoisseur the more time I spend here ( ‘Old-Fashioneds’ are the best….just one ice cube  though please, otherwise you can’t taste the tones of… insert tasting notes here). 

 
		class Stockist
                 		has_many :bourbons, through: :bourbon_stockists
		

		class BourbonStockist     - the join model
		  	belongs_to :bourbon
		  	belongs_to :stockist
		

		class Bourbon
		  	belongs_to   :distillery 
		  	has_many :stockists, through: :bourbon_stockists
		

               	class Distillery
 			has_many: stockists
			has_many :bourbons


The join model needed to have an attribute unique to the model/relationship between the two models it joins - Bourbon and Stockist. It took me a while to grasp this concept, but I eventually understood this to mean the attribute would relate to a particular bourbon and a particular stockist. For example, if I submitted a note on Stockist 3’s bourbon called ‘Jim Beam”, then this note would only be found in one row of the join table. This note would not be saved for every bottle of Jim Beam in every stockist.  I have discovered that I like to draw tables and concepts out before I begin building anything in order to visualise them more clearly. This was especially important at this stage, as my understanding of the join table had been so fuzzy. 

I started with what view pages and routes that I would need:

ROUTES:

stockists 
index page (with links to individual stockist show page)
show page - with a list of bourbons by that stockist (with links to bourbon show pages)
new page - add a new stockist to database (add their bourbons on a check box form)
edit page - change name or address of stockist with link to delete, edit bourbons in stock
   
bourbon 
index page (with links to individual bourbon show page)       
show page (with list of stockists that have it. link to edit) 
new page - add a bourbon to the database, add bourbon stockists, add distillery
edit page - change bourbon details with link to delete, and check box to select stockists 

distilleries  
index page (with links to individual distilleries) 
show page  (with links to individual bourbons) - edit and delete button
new page (add a distillery to the database)
edit page (change distillery details - with link to add a bourbon) 
                           
Users     /login  - log in to account 
            /logout  - log out of account 
            /signup  -sign up 
           
I created some tables to show the routes I would be using to make things super clear for me:
*insert pic one here* ![](https://ibb.co/jSdLtU)
[](https://ibb.co/jSdLtU)

I knew I had to  make use of a nested resource with the appropriate RESTful URLs. My nested resource also had to provide a FORM that relates to the parent resource.

I knew I had to create a nested resource on a one to many relationship so I chose Bourbon and Distillery.  An example of how it works:

We have the RESTful URL of /distilleries/1 ( the show page for the distillery with an ID of ‘1’)
If the user wanted to see all the bourbons created by this distillery, our nested resource would be:
 /distilleries/1/bourbons
The route /distilleries/1/bourbons/new would allow the user to create a new bourbon for distillery 1

 Additionally, I wanted the nested new bourbon page to have the option to add stockists .The show page would also have an edit and delete link for the bourbon.

By the end of the project, my routes.rb file actually ended up looking like this:
 insert pic 2 here  ![](https://ibb.co/hkNPL9) 
 
 In development, I decided that I would have to add routes for the BourbonStockist model if I wanted to include a user submittable form for the :notes attribute. I also wanted to create the ability to edit and delete the notes. 

I decided to add another controller too, after I had built the users_controller. I needed a welcome_controller with a get ‘/welcome’ route that took the user to a home page. I thought it would make for a better experience for the user to have a visible ‘home’ button where they could navigate to quickly. 

I spent a long time working on two issues in particular:

a) I was unable to create new notes  for BourbonStockists & the checkbox for stockists on the bourbon show page was not submitting properly.
I experimented with adding accepts_nested_attributes_for :bourbon_stockists to both Stockists and Bourbons and it still did not seem to work. I discovered one possible reason why - I had added the wrong validation to my model:
insert pic 3 here:
![](https://ibb.co/kVvdf9)
I didn’t want the User to have to submit a note every time they created a Stockist or a Bourbon. Removing this validation helped with creating, editing and showing notes but I was still unable to link multiple existing stockists to a new bourbon (or edit an existing bourbon with existing stockists). It turned out I had wasted time by not inspecting my params properly in my terminal. The message generated by SQL at the top of the terminal informed me that ‘Stockist’ was an unauthorised parameter. 
I checked my strong_params method in Bourbon model and sure enough I had not included it : 
insert pic 4 here:
![](https://ibb.co/ehoW09)
How had I not noticed that before? I felt pretty stupid. It also brought to may attention that in my desperation to solve the issue, I had tried to add a feature to my bourbon controller that I didn’t fully understand but really should be cognisant of when dealing with models and associations - 

accepts_nested_attributes_for
What is it for and when do I use it? 

“Nested Attributes is a feature that allows you to save attributes of a record through its associated parent."(https://www.pluralsight.com/guides/ruby-on-rails-nested-attributes) . 

This means I can create or edit an instance of a model through another model. 
If I wanted to create a new stockist through the new or edit bourbon pages, then I would add it in the model,  using  fields_for  in my form to generate the association fields.  I would then have new params keys, which would mean I have to modify my strong_params method in my controller to accept them.

We need to add a separate method to the class model when we want to avoid duplicates of the row we are creating. In this instance, we  would use the find_or_create_by in a model_attributes= method:

#app/models/song.rb
 
class Song < ActiveRecord::Base
  def artist_attributes=(artist)
    self.artist = Artist.find_or_create_by(name: artist.name)
    self.artist.update(artist)
  end
end
( example from the ‘Basic Nested Forms’ module)
 
…………it was at this point of writing my blog that I realised that I had misused ‘accepts_nested_attributes_for’ in some of my models. I had added it simply because I thought I needed it, but didn’t understand WHY i needed it. I went back through the code and noticed it several times:

insert pic 5 here
![](https://ibb.co/doZ4L9)
In my latest Github commits, you can see that I went back through my code removing the ‘accepts_nested_attributes_for  from two of my models. I decided to leave it in the bourbon model and create a section in my form where the user would have an option to create a stockist, at the same time as creating a bourbon. I used ‘fields for’ in my form, created a stockists_attributes= method in the Bourbon model, and made sure that my strong params accepted them. I’m glad I looked into this method before submitting the project. I removed a lot of unnecessary code and added a new feature. However, I had to remove the bourbon_stockist_attributes from my 

insert pic 6 here
![](https://ibb.co/hgpFSp)
bourbon_params. There was no need for it to be there. I wasn’t creating new notes ON the new bourbon page. 

b) The second  problem I came across was that, while I was able to create a user account, I then couldn’t log in as that user. I found that by adding a 
:user key in the find_by and .authenticate methods with the create method, it worked. I added the key of    [:user]     before    [:username]  & [:password]

insert pic 7 here

![](https://ibb.co/kQMUnp)

I found this project very challenging yet at the same time extremely fulfilling. I surprised myself by how much time I devoted to perfecting this project because I was so keen to get everything just right. I feel that I have learnt a great deal through overcoming problems I encountered along the way, which led to a deeper understanding of nested forms, validations and key names. Having said that, I am not yet 100% satisfied with my project and don’t by any means consider it ‘finished’. I would love to improve upon it in the future by DRYing up some of the controller code (especially in the Bourbons Controller) and  perhaps adding more helper methods to clean up some of the view pages.
 
 
