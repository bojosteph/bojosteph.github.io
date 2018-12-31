---
layout: post
title:      "My First Ruby CLI Project "
date:       2018-12-31 01:04:59 -0500
permalink:  my_first_ruby_cli_project
---






My first ruby CLI project tvshow.  The hardest part in creating a CLI project is to plan on creating your classes once you get your data from the API or website. I guess that's the key in all of this is understanding Objects and Classes and how you will use them  in your program. On this project, I used bundler to create my gem tvshow.  bundle gem tvshow . This made it easier to set up my gem by doing it this way. I also added my my gem dependency in the gemspec folder . on this project I'm using httparty to parse my api data, I added pry and colorize gem. pry is very helpful in seeing the data to help you create your objects and classes.

After some trial and error I am able to create my objects and started to have a better plan on what I want to do. It was not easy in the beginning but I learned a lot. The tvmaze api also allows you to do a search using fuzzy logic by adding query at the end like


.URL: /search/shows?q=:query

 Example: http://api.tvmaze.com/search/shows?q=girls

After creating my first two  Classes the tvapi class and show class and able to create my objects. I'm able to add my other classes. I'm able to create type class and genre class from the show hash. I'm able to add a Cast class by adding show id /embed= cast and use the additional data to get the cast of each show.

Using the objects  I was able to create it made it easier to get the information from the objects . I  can sort shows by name alphabetically, sort by type, sort by genre. sort show by rating. The user can interact using my cli application following prompts. And by adding some modification with my API class I was able to add search by keyword and list cast of the show by show id. using detect and select I'm able to get the object and print it out to the user

Check out my cli project on github

https://github.com/bojosteph/tvshow.git

Happy Coding


  
	
	
	

