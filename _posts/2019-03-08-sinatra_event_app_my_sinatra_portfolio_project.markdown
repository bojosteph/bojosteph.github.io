---
layout: post
title:      "Sinatra Event App My Sinatra Portfolio Project"
date:       2019-03-09 03:39:30 +0000
permalink:  sinatra_event_app_my_sinatra_portfolio_project
---

 




<br>
<br>


<iframe class="embed-responsive-item"id="ytplayer" type="text/html"   width="560" height="315" src="https://www.youtube.com/embed/yL4nFGtLwX0?&autoplay=1&loop=1&rel=0&showinfo=0&color=white&iv_load_policy=3&playlist=yL4nFGtLwX0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


<br>

<br/>
Building Sinatra Event App

Using The Lesson I learned from Building My CLI project and The CRUD application Lesson and Example from One of Our Flatiron Instructor I am able to Build My Sinatra Project called sinatra-event-app
<p>
https://sinatra-event-app.herokuapp.com
</p>
  
<br>
<br>

<p>The purpose of this Project is to Learn How to Build a Working Web App Using Sinatra That will  perform CRUD application using a database that will store  data from user input .  Using ruby I can get information from the database and present it to the user . I have to use the MVC pattern to organize my code and adhere to current practice for web application .<p> I want to use Active Record to get data from DB and use  migration to set  up my database and schema</p>
<br>

<p> I have decided to build a web app that will handle events like a mini event manager app .</p>
<p> <strong>User
<p>1.  User can be an Event Creator or an Event Participant via RSVP</p>
 <p>  .  A user is required to Sign-Up or Log-In to Access Account</p>
 <br>
 <p>2. As An Event Creator a User Should be able :</p>
    <p> .View all Events </p>
 <p>    .Create an Event</p>
<p>     . Update and Delete Event</p>
  <p>   .View User Own Event </p>
  <p>   .View Participants to Own Event</p>
 <p>    .Cancel RSVP event </p>
 <br>
   <p>  3. As an RSVP participant a User Should Be able:</p>
   <p>  .View all the events the user rsvp’d</p>
  <p>    .Cancel rsvp for event the user sign-up on</p></strong>
 <br>
<p>   Using Corneal I am able to generate my project structure . </p>
Using this gem made it easier to get started.
<p>You can gem install corneal  and use `corneal new name-of-app` to set up your file .</p>
<p> I Have experienced Issue with sqlite1.4 so I have to change my gemfile to sqlite 1.3.13 before running bundle install 
<br>
I want to see my model associations before I start going into details of how to set up views and controllers.<p> I want to see how I can access data from my database . I planned on using tux first to achieve this  . Tux is a ruby gem you can use that will let you use your terminal to create objects and access database to plan and see if everything will work before you go deep in your programming.
<br>






I created my models first 
my user class 
user.rb 

```
class User < ActiveRecord::Base
        has_secure_password
        validates_presence_of :username, :email, :password, :full_name
         has_many :events
        has_many :rsvp_events
        end
```
  
```
event.rb
class Event < ActiveRecord::Base
 validates_presence_of :name, :date, :location, :description
 belongs_to :user
 has_many : rsvp_events
end
```
```

```
```
rsvp_event.rb

class RsvpEvent < ActiveRecord::Base
 belongs_to :event
 belongs_to :user
End
```
```



```
Using rake-T I was  able to see list of available commands  and I am  able to run my migration . In the end my schema looks like this 
```


ActiveRecord::Schema.define(version:) do

 create_table "events", force: :cascade do |t|
   t.string   "name"
   t.string   "date"
   t.string   "location"
   t.string   "description"
   t.datetime "created_at",  null: false
   t.datetime "updated_at",  null: false
   t.integer  "user_id"
 end


 create_table "rsvp_events", force: :cascade do |t|
   t.integer "event_id"
   t.integer "user_id"
 end

 create_table "users", force: :cascade do |t|
   t.string   "username"
   t.string   "email"
   t.string   "password_digest"
   t.datetime "created_at",      null: false
   t.datetime "updated_at",      null: false
   t.string   "full_name"
 end

end

```

After I got this set Up I can run 
```

rake db:migrate 

rake db:seed


```

After Playing in the terminal with Tux and got my associations working . I have a better understanding of how to set up my routes and views so  its time to set up my controller and views . 
```

 



```
For my Controllers . The rest of the controllers will inherit from application controller . 

 Apllication Controllers : This will inherit from Sinatra::Base middleware , set up sessions secret and Sinatra flash , I will also put my helpers method here to help with user authentication 
```

```
<br>
<br>
```
require './config/environment'

class ApplicationController < Sinatra::Base
 configure do
   set :public_folder, 'public'
   set :views, 'app/views'
   register Sinatra::Flash
   enable :sessions
   set :session_secret, ENV.fetch('SESSION_SECRET')
 end

 get '/' do
   erb :"/index.html"
 end

 helpers do
   def current_user
     session[:user_id] && User.find_by(id: session[:user_id])
   end

   def logged_in?
     !!current_user
   end
 end
end
```
```




```
<p>  I Have  3 other controllers
<p>  UsersControllers this will define Restful routes relevant to the user
<p>  EventsControllers this will define Restful routes relevant to an Event
<p>  RsvpEventsControllers this will define Restful routes relevant to an Rsvp event.
```


```

Time to Set Up The Views . I started with layout.erb that will be my template with navbar and index.html.erb that will welcome user and has log in and create acccount 

<p>  I put a lot of work on the layout using  bootsrap 4 and then adding a navbar with ruby code to set up different nav set up if the user is  logged or not logged in .
<p>Check out my layour.erb 





```
layout.erb 




<body>

 <nav class="navbar navbar-expand-sm navbar-dark bg-dark">
   <a class="navbar-brand" href="/">Sinatra Event App</a>
   <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavDropdown" aria-controls="navBarNavDropdown"
     aria-expanded="false" aria-label="Toggle navigation">
     <span class="navbar-toggler-icon"></span>
   </button>
   <div class="collapse navbar-collapse" id="navbarNavDropdown">
     <ul class="navbar-nav">
       <% if logged_in? %>
       <li class="nav-item active">
         <a class="nav-link" href="/events">Upcoming Events</a>
       </li>
       <li class="nav-item">
         <a class="nav-link" href="/events/new">Create Events</a>
       </li>
       <li class="nav-item">
         <a class="nav-link" href="/logout">Log Out</a>
       </li>
```

```
```
```

      ```
 ```
<li class="nav-item dropdown">
         <div class="btn-group">
           <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownMenuLink" data-toggle="dropdown"
             aria-haspopup="true" aria-expanded="false">
             Dropdown link
           </a>
           <div class="dropdown-menu" aria-labelledby="navbarDropdownMenuLink">
             <a class="dropdown-item" href="#">Action</a>
             <a class="dropdown-item" href="/events">Upcoming Events</a>
             <a class="dropdown-item" href="/events/new">Create Events</a>
             <% @user = current_user %>
             <a class="dropdown-item" href="/users/<%= @user.id %>">Your Events</a>
             <div class="dropdown-divider"></div>
             <a class="dropdown-item" href="/rsvp_events">Events You Rsvp</a>
             <a class="dropdown-item" href="/logout">Log Out</a>
           </div>
         </div>
       </li>
```
```

      ```
 ```
<% end %>
       <% if !logged_in? %>
       <li class="nav-item">
         <a class="nav-link" href="/login">Log In</a>
       </li>
       <li class="nav-item">
         <a class="nav-link" href="/signup">Sign Up</a>
       </li>
       <% end %>
     </ul>
   </div>

 </nav>
```
```


```

 ```
<%= styled_flash%>
 <%= yield %>
```
```



 
```
```
</body>

</html>
```

The rest of my view will be able to use layout.erb  because of yield making it easier to focus on the body of each page . 

I have learned alot with this project but I also enjoyed the building process once I got things working and have my plan in place.
In the end we all want to learn and be good at being a web developer so embrace the journey

I also encountered a lot of issues with my local environment set up which is frustrating with windows set up . But once I set up Virtualbox and start using Vscode and Ubuntu   I will never go back .  There is a guide in learn about  setting up  your Local  environment  using virtual Machine for Windows and set up for Mac user .

Also Check out This Helpful Guide about deploying Your Sinatra app to Heroku 
 from our Flatiron Instructor Dakota Martinez to get your app up and running in Heroku 
 I included a link below 
 
 
[]http://github.com/DakotaLMartinez/sinatra-heroku-demo.git)


Styling you Web App using Bootstrap helps with media query to make sure your app will have a consistent look in different device and will collapse and line up so user can still view your view  in smaller device .
There is plenty of guide in styling your forms , input and use of buttons .

<p>Using HTML  input attributes in your form will help with  user side validation adding to your server side validation with less code . 
Example form below  . Add required on each field and the browser will alert the user of missing field and will not submit the form until its filled out .

```
<div class="container">
 <h1 style="padding-top: 10px; padding-bottom: 10px;">Log In</h1>
```

 ```
```
```
<form  action="/login" method="POST">
   <div class="form-group">
     <label for="username">Username</label>
     <input type="text" class="form-control" id="username" name="username" required placeholder="Enter username">
   </div>
   <div class="form-group">
     <label for="password">Password</label>
     <input type="text" class="form-control" id="password" name="password" required placeholder="Enter password">
   </div>
   <button type="submit" class="btn btn-primary btn-lg btn-block">Log In</button>
```
```

 ```
```
</form>
</div>
```
```
```

Working with Sinatra Gave Me a better understanding of How things work in the background and Where to look for issues .

Check out my repo  in github

[]https://github.com/bojosteph/sinatra-event-app.git)

<p><sttrong>Things to improve in the future 
<p> User can search events
<p> User can review rsvp events after attending
<p> Add more features and functionality to make this a Full Pledge Event Manager

<p> Thanks and Happy Coding !
  

 



       

      
       
         






