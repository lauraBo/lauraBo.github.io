---
layout: post
title:      " The Github Humane Society"
date:       2018-06-20 17:21:04 +0000
permalink:  the_github_humane_society
---


For my Sinatra project, I created an app called ‘**Find my New Best Friend**’ which allows dog shelter employees to sign up using secure personal accounts to create adoptable dog listings. Users also have the ability to edit and delete the listings they have created. Registered users can also view their home page with all the dog listings they have created.Each user must be logged in to have an access to their content. Unregistered web users can view the public index page with all adoptable dogs listed by all dog shelters. 

I wanted to prepare as well as I could before diving in, so I created a sort of flow chart to help me:

*Unregistered Users *can:

visit the welcome page    ‘/‘    where they can click on the link to the public dog index which lists all dogs  
 ‘/dogs’


*Shelter Staff *can :

visit the welcome page    ‘/‘
    	where they can :  		- view the public dogs index ( ‘/dogs’ )
   						- log in      (‘/login’)
   						- sign up  (‘/signup’)
visit the log in page       ‘/login’
   	 where they can:		 - log in  with their details 
    						- go back to welcome page  ( ‘/‘ )           

visit the sign up page  ‘/signup’
          where they can: 		-create a new account
   						 - click link to log in if already a member (‘/login’)
                                          	-  click link to public dog index if not shelter staff (‘/dogs)
     
visit their Users homepage   ‘/users/dogs’
  	  where they can:      	-view list of the user’s dogs   
  						- click link to create new dog                 (‘/dogs/new’)
  						-click link to log out                                (‘/logout’)
   						-click link to see the public dog index    (‘/dogs’) 
visit individual dog show page        /dogs/:id'      
           where they can:             - see one particular dog                          
						-delete the particular dog listing

visit update page                        ‘/dogs/:id/edit’
          where they can: 		-see current dog details
						-update dog details 

  

I used the **Corneal** ruby gem to create my file framework and I found it very simple to install . Thank you to Brian Emory for creating this ruby gem. I have a bit of a phobia about creating the initial directory and framework required for these projects and it helped a lot!

I then made sure to add the use Rack::MethodOverride to my config.ru file so that my app would know how to handle patch and delete requests. 

The very first stumbling block I came across was when I was creating my initial migration files. I had planned to create 3 classes : User , Dog and Shelter. However, when I had to state the relationship between the three classes, I started to worry that I was creating something too complex ( for me). **Could a class belong_to two classes**?



Dog belongs_to Shelter
Dog belongs_to User 

I knew that this was possible, but it brought up confusion for me in regards to the foreign key. I wanted an instance of a Dog to have a user_id so that only that particular user could edit or delete that instance. If it belonged to a shelter, then the dog instance would also need a shelter_id. However, a user would already  be a part of a shelter so wouldn’t this mean the Shelter Class was unnecessary? Ultimately, I decided to make ‘shelter’ an attribute of the Dog class instead of a separate class. On reflection,  If I were to build this app again, I would build Shelter as a separate class. I think I would also add a complex form to the create new dog form,  so that every time a dog instance is created, there are tick boxes to associate a particular shelter with a dog.  

After creating my migration files and models, I then used tux in the terminal to create and associate instances of the dog class with users.  I then moved into the next phase of building the routes, views and forms that would allow users to interact with my app. 


 SEED DATA….    

I started to fill up a seed file with data, but then was unsure about whether I needed to manually add ‘user_id’ data to the file, or whether this would be done automatically when I ran the file. I decided not to run ‘ rake db:seed’ as I was worried I would mess up my database with invalid data.  I decided to add my data ( sign up as different users and create dog instances)  on the app instead, using shotgun. 

The next step was creating the ROUTES and CONTROLLERS.  Here is a table I created to help me understand the different routes and actions needed in my app: 

![](https://imgur.com/a/3wau1VF)

DOGS CONTROLLER 

Firstly, I set up the root path and the home view page. I then started on the CREATE part of my CRUD app by setting up the ability to create a new dog.The get ‘/dogs/new'  route  renders the dogs/new.erb view.  I also created the index.erb file so I could test out whether the form would be successfully submitted. Once this was working ok I set up another controller action, post ‘/dogs'  where I placed the code that extracts the form data from the params to create a new instance of the dog class. 

READ
My table shows that the Read CRUD action corresponds to two different controller actions: show and index.  I created the view show.erb file, which shows an individual dog. The index action should render the erb view index.erb, which shows a list of all of the dogs.

Active Record needs to grab all of the dog instances and store them in an instance variable, so I created @dogs. I used erb in  the dogs/index.erb view  to iterate over @dogs and render them successfully on the page.

I then created the get ‘/dogs/:id' controller action. This action grabs the dog with the id in the params and sets it equal to the instance variable @dog . The show.erb view page also uses erb to render the @dog’s details.

UPDATE
Next, I created a controller action, get ‘/dogs/:id/edit', and the view, dogs/edit.erb. This view contains a form to update a specific dog and POSTs to a controller action, patch ‘/dogs/:id'. When I tried this controller action on the app using shotgun, I kept getting error messages that I didn’t fully understand. I thought that my redirect route was wrong so I changed it to homepage rather than /dogs/:id’. I still got the same error message though so I figured something must be wrong with the edit form itself. Sure enough, I had made a small punctuation error in the input part of the form. I changed it to read: 

<input id="hidden" type="hidden" name="_method" value="patch">


DELETE
I then created the  ‘/dogs/:id/delete' route in the controller and added a "delete button" to the show page.  In retrospect, perhaps I should have created a flash message to tell the user they had successfully deleted the listing. 

I then started on user authentication . I created helper methods in the Application Controller for this purpose which located the correct user and then set the :idkey in the session hash equal to their user ID.

I  created two  routes  in Users Controller :

The    get '/logout' which is responsible for logging the user out by clearing the session hash,
and the  route   get  '/users/home'  which is responsible for rendering the user's homepage view when they have successfully logged in or signed up. I created an instance variable @user to access the current user in the view page.

It was at this point  of the project that I ran into some trouble that delayed me for a few days. When I went to open the IDE to work on my project I saw that a bulk of my files in the directory had disappeared. When I typed ‘git status’ I saw that they had been deleted. Had I done it accidentally? I began to panic that I had saved my project in the wrong place, somewhere where I wasn’t supposed to ,and someone had deleted them. One thing is for sure, **I need an intense 101 on Github**! The episode brought to my attention that I don’t have a clue about Github or its terminology.  I’m actually pretty scared of it now so I need to work on that! in my efforts to get my project back,  I opened branches, turned into some kind of ‘remote head’ , couldn’t save files to the master, and cloned I don’t know how many of the wrong repos. I felt like I was crawling down a rabbit hole and felt useless. I googled how to revert back to a previous commit but in a panic couldn’t follow the instructions properly and ended up in another tree. I spoke to a lovely Learn Instructor who showed me how to revert back to a  previous commit successfully. I have bookmarked the page should it happen again. 
 
Once I had my project back , I added flash messages to some of the routes in both the dogs controller and the users controller but they didn’t work when I ran shotgun.  The reason was simple enough - I had forgotten to add erb at the top of the view pages. 

After creating the app, I asked myself whether I created the routes in the right order. Should I have created the user sign in and log in first? In other words, Is it best to set up the authentication part of an app before creating the CRUD routes? I suppose the only way I can answer that is by creating another CRUD app and giving it a try to see which is best. 

**Post project research:**

Is it better to have an error view page to redirect to,  or just use flash messages?

Could I show the number of dogs currently in the index view page using ‘Dog.all.size’?

When you seed data do you need to manually add the foreign key? 

How do you overcome a phobia of GitHub ? :-) 
