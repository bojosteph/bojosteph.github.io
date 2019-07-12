---
layout: post
title:      "My Rails JS Project"
date:       2019-07-12 02:56:49 +0000
permalink:  my_rails_js_project
---


When I started  working on this Project I was using my existing views from my Rails project and I had a very difficult time implementing what I want to do .  I really like working with JS . I find it very powerful and enjoyable to work with. The issue with JS is that it can behave very differently compared to ruby . In order to work with JS I have to learn about call stack and event loop , lexical scope which up to  this point I still don't have a firm understanding <br><br>With JS its important where you write the function to get access to the variables except in a situation where you are dealing with this . With this it's where you call the function . if you type this in the console it will give you the window object .<br>In JS you can wrap a function with another function , assign a function to a variable and call that variable . ES6 added classes which can help you organize your code and use constructor method which gets initialized when you call  new  . So understanding this a little bit help me write functions that helped me implement my project and I was able to redo my rails app using JS  as the frontend and rails providing the API.<br><br> I  used fetch which return a promise object which can be resolved or rejected and both of that is considered a successful result so you can create methods to handle parsing the data or catching errors.<br> After you get the data from the API using fetch and promise you can plan on how you will handle the response you call a method on it right away and append it to the DOM , you can store it on an Array or you can design classes and use methods from that class to render the data you want . <br><br>Another important thing about JS is that its a single thread programming language . So it means its synchronous . The web API allows JS to be asynchronous because it can pass the methods that its not handling and  once it's resolved its get added back to the stack from the event loop allowing JS to run in the browser smoothly . <br><br>
I have a better understanding of targeting element and using evenListeners to set up my view .
In the end I was able to get my app behaving like a crud application but I wish I had more time to add Calendar functionality to it . Maybe Next Time. Happy Coding 



