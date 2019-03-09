---
layout: post
title:      "Sinatra Event App My Sinatra Portfolio Project"
date:       2019-03-08 22:39:31 -0500
permalink:  sinatra_event_app_my_sinatra_portfolio_project
---




![](http://)<iframe width="560" height="315" src="https://www.youtube.com/embed/yL4nFGtLwX0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
 









Building Sinatra Event App

Using The Lesson I learned from Building My CLI project and The CRUD application Lesson and Example from One of Our Flatiron Instructor I am able to Build My Sinatra Project called sinatra-event-app
<p>
<a href="https://sinatra-event-app.herokuapp.com">sinatra-event-app</a>
</p>
  


<p>The purpose of this Project is to Learn How to Build a Working Web App Using Sinatra That will  perform CRUD application using a database that will store  data from user input .  Using ruby I can get information from the database and present it to the user . I have to use the MVC pattern to organize my code and adhere to current practice for web application. I want to use Active Record to get data from DB and use  migration to set  up my database and schema</p>



<p> I have decided to build a web app that will handle events like a mini event manager app .</p>
<p> <strong>User</p>
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
 
   <p>  3. As an RSVP participant a User Should Be able:</p>
   <p>  .View all the events the user rsvp’d</p>
  <p>    .Cancel rsvp for event the user sign-up on</p></strong>

<p>   Using Corneal I am able to generate my project structure . </p>
Using this gem made it easier to get started.
<p>You can gem install corneal  and use `corneal new name-of-app` to set up your file .</p>
<p> I Have experienced Issue with sqlite1.4 so I have to change my gemfile to sqlite 1.3.13 before running bundle install </p>

<p>I want to see my model associations before I start going into details of how to set up views and controllers.</p> I want to see how I can access data from my database . I planned on using tux first to achieve this  . Tux is a ruby gem you can use that will let you use your terminal to create objects and access database to plan and see if everything will work before you go deep in your programming.</p>






I created my models first 

my user class 

```
user.rb 

class User < ActiveRecord::Base
  has_secure_password
  validates_presence_of :username, :email, :password, :full_name
  has_many :events
  has_many :rsvp_events
end
```


  
<code>
<p>event.rb</p>
<p>class Event < ActiveRecord::Base</p>
<p> validates_presence_of :name, :date, :location, :description</p>
 <p>belongs_to :user</p>
<p> has_many : rsvp_events</p>
<p>end</p>
</code>

<code>
rsvp_event.rb

<p>class RsvpEvent < ActiveRecord::Base</p>
 <p>belongs_to :event</p>
 <p>belongs_to :user</p>
<p>end</p>
</code>



Using rake-T I was  able to see list of available commands  and I am  able to run my migration . In the end my schema looks like this 


<code>
<p>ActiveRecord::Schema.define(version:) do</p>

<p> create_table "events", force: :cascade do |t|</p>
 <p>  t.string   "name"</p>
 <p>  t.string   "date"</p>
<p>   t.string   "location"</p>
<p>   t.string   "description"</p>
 <p>  t.datetime "created_at",  null: false</p>
<p>   t.datetime "updated_at",  null: false</p>
 <p>  t.integer  "user_id"</p>
<p> end</p>
 </code>
 
<code>
<p> create_table "rsvp_events", force: :cascade do |t|</p>
<p>   t.integer "event_id"</p>
<p>   t.integer "user_id"</p>
<p> end</p>
 </code>

<code>
 <p>create_table "users", force: :cascade do |t|</p>
  <p> t.string   "username"</p>
 <p>t.string   "email"</p>
 <p> t.string   "password_digest"</p>
 <p> t.datetime "created_at",      null: false</p>
  <p> t.datetime "updated_at",      null: false</p>
 <p>  t.string   "full_name"</p>
<p> end</p>
</code>





After I got this set Up I can run 


<p>rake db:migrate </p>

<p>rake db:seed</p>




<p>After Playing in the terminal with Tux and got my associations working . I have a better understanding of how to set up my routes and views so  its time to set up my controller and views . </p>


 



<p>For my Controllers . The rest of the controllers will inherit from application controller . </p>


 <p>Apllication Controllers : This will inherit from Sinatra::Base middleware , set up sessions secret and Sinatra flash , I will also put my helpers method here to help with user authentication </p>




<p>  I Have  3 other controllers</p>
<p>  UsersControllers this will define Restful routes relevant to the user</p>
<p>  EventsControllers this will define Restful routes relevant to an Event</p>
<p>  RsvpEventsControllers this will define Restful routes relevant to an Rsvp event.</p>




<p>Time to Set Up The Views . I started with layout.erb that will be my template with navbar and index.html.erb that will welcome user and has log in and create acccount </p>


<p>  I put a lot of work on the layout using  bootsrap 4 and then adding a navbar with ruby code to set up different nav set up if the user is  logged or not logged in .</p>


<p>The rest of my view will be able to use layout.erb  because of yield making it easier to focus on the body of each page . </p>


<p>I have learned alot with this project but I also enjoyed the building process once I got things working and have my plan in place.
In the end we all want to learn and be good at being a web developer so embrace the journey</p>


<p>I also encountered a lot of issues with my local environment set up which is frustrating with windows set up . But once I set up Virtualbox and start using Vscode and Ubuntu   I will never go back .  There is a guide in learn about  setting up  your Local  environment  using virtual Machine for Windows and set up for Mac user .</p>


<p>Also Check out This Helpful Guide about deploying Your Sinatra app to Heroku 
 from our Flatiron Instructor Dakota Martinez to get your app up and running in Heroku 
 I included a link below</p>
 
 
 
<p><a href="http://github.com/DakotaLMartinez/sinatra-heroku-demo.git">git hub sinatra-heroku-demo</a></p>



<p>Styling you Web App using Bootstrap helps with media query to make sure your app will have a consistent look in different device and will collapse and line up so user can still view your view  in smaller device .
There is plenty of guide in styling your forms , input and use of buttons .</p>


<p>Using HTML  input attributes in your form will help with  user side validation adding to your server side validation with less code . 
.If You Add required on each field , the browser will alert the user of missing field and will not submit the form until its filled out .</p>






<p>Working with Sinatra Gave Me a better understanding of How things work in the background and Where to look for issues .</p>


<p>Check out my repo  in github</p>


<p><a href="https://github.com/bojosteph/sinatra-event-app.git">github sinatra-event-app</a></p>


<p><strong>Things to improve in the future </p>
<p> User can search events</p>
<p> User can review rsvp events after attending</p>
<p> Add more features and functionality to make this a Full Pledge Event Manager</p>

<p> Thanks and Happy Coding !</p>


 
 



       

      
       
         







