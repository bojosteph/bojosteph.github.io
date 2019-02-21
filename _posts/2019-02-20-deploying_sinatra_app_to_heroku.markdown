---
layout: post
title:      "Deploying Sinatra App to Heroku"
date:       2019-02-21 00:50:09 +0000
permalink:  deploying_sinatra_app_to_heroku
---



<p>
Heroku is a Cloud platform as a service (PaaS). Anyway it's a popular cloud platform to deploy your app and it's free to use for basic service. 
</p>
<br>
<p>
When you are developing your app on a  local environment and start to deploy it on Heroku and your app is not Production Ready , I found out you will have a lot of things that will not work as planned. 
</p>
First Install Heroku CLI toolbelt in your system if you have linux or Mac its a lot easier than windows .<p> you can brew install or snap install depending on your system.</p>
<br>
Create  a Heroku Account and  do heroku login in your system
<br>
  Heroku uses a different database Postgres and the one I’m using locally sqlite3.
	<br>
You can change your Gemfile to use Postgres
Instead of 
<br>
`gem  ‘sqlite3`’
To 
`gem ‘pg’`
Run 
`$ bundle install `

Specify your ruby version
`ruby  “2.6.0”`

Initialize git repo
And do your commit
Run 
`$ heroku create`
and deploy  your app with
`git push heroku master`
If Things don't go right the first time  don't get discouraged .
<br>
If everythings goes right you can see your app deploy with 
<br>
`heroku open`  in your terminal 



