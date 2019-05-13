---
layout: post
title:      "Rails Portfolio Project"
date:       2019-05-12 23:28:26 -0400
permalink:  rails_portfolio_project
---

<br>

 <iframe width="560" height="315"
	  src="https://www.youtube.com/embed/exzlCZwQKFY?&autoplay=1&loop=1&rel=0&showinfo=0&color=white&iv_load_policy=3&playlist=exzlCZwQKFY" frameborder="0"
	   allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

<br>
    <a href="https://rails-event-app.herokuapp.com/" >RAILS EVENT APP </a>
<br>

<br>
My Portfolio project for Rails is Rails-Event-App . 
<br>
This Project is an extension of my sinatra project . I  started  using my own  controller and views  to Sign up. Sign in and Authenticate my user and then added  omniauth gem  to let user signin using facebook but later switched to devise  so I can be familiar with this popular gem for user authentication and sign up and sign in .The devise gem has very good ducumentaion and have a lot of resources . I have to add this code to add strong params with .my user model for my extra params like  user name  
<br>

```
class ApplicationController < ActionController::Base
  before_action :configure_permitted_parameters, if: :devise_controller?

  private

  def configure_permitted_parameters
    devise_parameter_sanitizer.permit(:sign_up, keys: [:username, full_name])
  end
end
```


My application has an Event model a User model ,  a join model of RsvpEvents and Reviews . I also have a Category model . 
My user class Has 3 different  types planner, participant and reviewer to make it easy to associate a user with the task .
I have to add a foreign key to my joint model using the different user type . this  is an example of my model and database ..On my event table I have the planner_id, on my rsvp_event i have the participant id and on my review class i have my reviewer_id 

```
Events table 

class CreateEvents < ActiveRecord::Migration[5.2]
  def change
    create_table :events do |t|
      t.string :name
      t.string :location
      t.string :description
      t.integer :planner_id
      t.datetime :start_date
      t.datetime :end_date

      t.timestamps
    end
  end
end
```

```
class Event < ApplicationRecord

  belongs_to :planner, class_name: 'User', foreign_key: 'planner_id'
  belongs_to :category

  has_many :rsvp_events, foreign_key: :attending_event_id, dependent: :destroy
  has_many :participants, through: :rsvp_events, source: :user

class User < ApplicationRecord
 
  has_many :events, foreign_key: 'planner_id'
  has_many :rsvp_events, foreign_key: :participant_id
  has_many :attending_events, through: :rsvp_events, source: :event
```
  
And  example of my  joint table model 

```
class RsvpEvent < ApplicationRecord
  belongs_to :attending_event, class_name: 'Event', foreign_key: 'attending_event_id'
  belongs_to :participant, class_name: 'User', foreign_key: 'participant_id'
 end
```

After setting my classes and associations I  started  working on my routes and model validations to help me set up my views .
I started nesting events under user but later changed it so I don't  have to use user id on my controllers and views .
I have nested  rsvp_events and reviews under events .

I have to add model validation for overlapping events and have to use scope method to prevent a user to create an event if  it overlaps to the user own event . other user can create event at the same time becuase its not overlapping thier events  . I tried different query methods but the following code worked the best 

```
scope :overlapping, lambda { |start_date, end_date|
    where(
      'start_date <= :end_date AND :start_date <= end_date',
      start_date: start_date, end_date: end_date
    )
  }

  def no_overlapping_events
    event = Event.overlapping(start_date, end_date)
    overlaps = event.where('planner_id = ?', planner_id)

    if overlaps.any?
      dates = overlaps.map do |e|
        [e.start_date.strftime('Start Of Event : %A, %b %e, at %l:%M %p'), e.end_date.strftime('End Of Event : %A, %b %e, at %l:%M %p')].join(' to ')
      end.join(', ')
      errors.add(:base, "must not overlap existing events. Overlaps: #{dates}")
    end
  end
```

That was the hardest to work on but it did the trick for me . I added it to my Event Validation to prevent creating an event so I don't  have to put that in my controller and I can prolpt he user for the error before creating the event .

```
class Event < ApplicationRecord

validate :date_must_be_current, if: :has_date_range?
 validate :correct_date_range, if: :has_date_range?
 validate :no_overlapping_events, on: :create
```


By validating on create  only . I can still edit my event . if I just put validate It will also affect me editing the particular event .

A user as planner can create an event . as a participant a user  can rsvp to an event and as a reviewer a user  can review an event 

I have added logic on my buttons on the  show page to allow a user to rsvp but the other button is not accessible until the user  rsvp . I have to guard on some null or nill  values on my views and i find out using  .blank? Work better than nil? Or empty? 

```
<% unless @rsvp_event.blank? %>
  do something ….
<%end %>
```

This helps with my controller option also 
<br>
Overall . I was able to accomplish in adding extra features I wish i have for my sinatra app .
I’m looking forward to adding extra functionality with javascript and jquery
<br>
below is a link to my github 

<br>

<a href="https://github.com/bojosteph/rails-project-event-app.git">github rails-event-app</a>

