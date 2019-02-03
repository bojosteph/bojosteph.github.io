---
layout: post
title:      "Sinatra Routes"
date:       2019-02-03 19:59:59 +0000
permalink:  sinatra_routes
---






Sinatra is a domain specific language a lightweight version of Rails that is available to use as a Ruby Gem to create Web Applications. A good simple example to is output “Hello World” to the local Browser .


To use


Install the gem:

`gem install sinatra`



Require Sinatra in your Application


```
# sinatra.rb
require 'sinatra'
```



And set up your routes in your application by  get an HTTP paired with a URL-matching pattern

Associated with a block


```
get '/' do
 'Hello world!'
end
```


Or


```
get '/goodbye' do
 'Goodbye See You Later!'
end
```



And you can Run Your Application with
`ruby sinatra.rb`


View at: http://localhost:4567


View the other route at http://localhost:4567/goodbye


I like using Sinatra and I am  looking forward on developing my first Web App Using this framework .

Happy Coding









