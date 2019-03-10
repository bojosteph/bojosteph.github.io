---
layout: post
title:      "Sinatra Event App My Sinatra Portfolio Project"
date:       2019-03-08 22:39:31 -0500
permalink:  sinatra_event_app_my_sinatra_portfolio_project
---



<p> </p>
<iframe width="560" height="315" src="https://www.youtube.com/embed/yL4nFGtLwX0?&autoplay=1&loop=1&rel=0&showinfo=0&color=white&iv_load_policy=3&playlist=yL4nFGtLwX0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


<p> </p>



Building Sinatra Event App

Using The Lesson I learned from Building My CLI project and The CRUD application Lesson and Example from One of Our Flatiron Instructor I am able to Build My Sinatra Project called sinatra-event-app

<br>
<a href="http://sinatra-event-app.herokuapp.com">Sinatra Event App</a>
<br>

The purpose of this Project is to Learn How to Build a Working Web App Using Sinatra That will perform CRUD application using a database that will store data from user input . Using ruby I can get information from the database and present it to the User . I have to use the MVC pattern to organize my code and adhere to current practice for web application. I want to use Active Record to get data from DB and use migration to set up my database and schema

<br>

I have decided to build a web app that will handle events like a mini event manager app .

User
<ul>

<li>User can be an Event Creator</li>
<li>User can be Event Participant via RSVP</li>
<li>A user is required to Sign-Up or Log-In to Access Account</li>
</ul>
<br>
User as Event Creator Should Be able to 
<ul>
<li>View all Events</li>
<li>Create an Event</li>
<li>Update and Delete Event</li>
<li>View User Own Event</li>
<li>View Participants to Own Event</li>
<li>Cancel RSVP event</li>
</ul>
<br>
As an RSVP participant a User Should Be able to
<ul>
<li>View all the events the user rsvp’d</li>
<li>Cancel rsvp for event the user sign-up on</li>
</ul>
<br>
<p>Using Corneal I am able to generate my project structure .Using this gem made it easier to get started.

You can gem install corneal and use `corneal new name-of-app` to set up your file .</p>
<p>Run Bundle install and you are ready to go . If You encounter inssue during install check if changing sqlite3 version to lower version from 1.4 will help. I have to change mine from 1.4 to 1.3.13 on my gemfile and run bundle install again</p>
<br>
<p>I want to see my model associations before I start going into details of how to set up views and controllers.</p>
<p>I want to see how I can access data from my database . I planned on using tux first to achieve this . Tux is a ruby gem you can use that will let you use your terminal to create objects and access database to plan and see if everything will work before you go deep in your programming.</p>

<p> I have Created 3 Models for my program  the first model I have is the User Class, Followed by Event and Rsvp_Event Class </p>

```
user.rb 

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
rsvp_event.rb

class RsvpEvent < ActiveRecord::Base
  belongs_to :event
  belongs_to :user
end
```
<br>

Using rake -T,  I was able to see list of available commands and I am able to run my migration . In the end my schema looks like this
<br>

```
ActiveRecord::Schema.define(version:) do

 create_table "events", force: :cascade do |t|
   t.string   "name"
   t.string   "date
   t.string   "location"
   t.string   "description"
   t.datetime "created_at",  null: false
   t.datetime "updated_at",  null: false
   t.integer  "user_id"
 end
```


```
create_table "rsvp_events", force: :cascade do |t|
   t.integer "event_id"
   t.integer "user_id"
 end
```

```
create_table "users", force: :cascade do |t|
  t.string   "username"
  t.string   "email"
  t.string   "password_digest"
  t.datetime "created_at",      null: false
  t.datetime "updated_at",      null: false
  t.string   "full_name"
 end
```

<br>
After  I got this set Up I can run

`rake db:migrate `  and `rake db:seed`


<p>After Playing in the terminal with Tux and got my associations working . I have a better understanding of how to set up my routes and views so its time to set up my controller and views .</p>

<p>For my Controllers . The rest of the controllers will inherit from application controller .</p>

<p>Apllication Controllers : This will inherit from Sinatra::Base middleware , set up sessions secret and Sinatra flash , I will also put my helpers method here to help with user authentication</p>

<p>I Have 3 other controllers</p>



<p>UsersControllers this will define Restful routes relevant to the user</p>

<p>EventsControllers this will define Restful routes relevant to an Event</p>

<p>RsvpEventsControllers this will define Restful routes relevant to an Rsvp event.</p>

<p>
Time to Set Up The Views . I started with layout.erb that will be my template with navbar and index.html.erb that will welcome user and has log in and create acccount</p>


<p>I put a lot of work on the layout using bootsrap 4 and then adding a navbar with ruby code to set up different nav set up if the user is logged or not logged in . This way the User can access different navigation control if logged in and if not logged in will have limited nav set up. This will also Help with better User experience .</p>
<p>The rest of my view will be able to use layout.erb because of yield making it easier to focus on the body of each page .</p>
<p>I have learned a lot with this project but I also enjoyed the building process once I got things working and have my plan in place . In the end I  want to learn and become a better web developer. So  I am embracing this  journey</p>

<p>I also encountered a lot of issues with my local environment set up which is frustrating with windows set up . But once I set up Virtualbox and start using Vscode and Ubuntu I will never go back . There is a guide in learn about setting up your Local environment using virtual Machine for Windows and set up for Mac user .</p>

<p>Also Check out This Helpful Guide about deploying Your Sinatra app to Heroku from our Flatiron Instructor Dakota Martinez to get your app up and running in Heroku I included a link below</p>
<p><a href="https://github.com/DakotaLMartinez/sinatra-heroku-demo.git">Sinatra Heroku Demo</a></p>

<p>Styling you Web App using Bootstrap helps with media query to make sure your app will have a consistent look in different device and will collapse and line up so user can still view your view in smaller device . There is plenty of guide in styling your forms , input and use of buttons .</p>

<p>Using HTML input attributes in your form will help with user side validation adding to your server side validation with less code . .If You Add required on each field , the browser will alert the user of missing field and will not submit the form until its filled out .</p>

<p>Working with Sinatra Gave Me a better understanding of How things work in the background and Where to look for issues if the program breaksdown</p>

<p>Check out my repo in github</p>

<p><a href="https://github.com/bojosteph/sinatra-event-app.git">git hub Sinatra-Event-App</a></p>

<p>Things to improve in the future </p>

<p>User can search for events</p>

<p>User can review rsvp events after attending</p>
<p>Add Event type and zipcode so App can  list Event by location and type of events</p>

<p>Add more features and functionality to make this a Full Pledge Event Manager</p>

Thanks and Happy Coding !
























