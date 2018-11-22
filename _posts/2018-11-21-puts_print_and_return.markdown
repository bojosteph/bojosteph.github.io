---
layout: post
title:      " Puts, Print and Return"
date:       2018-11-21 20:19:39 -0500
permalink:  puts_print_and_return
---





</style>

<div class="container">
<p>both puts and print output to the console but return nil values</p>
<p> the difference between print and puts is that puts  add a newline character</p>
<p></p>
<p>In the following example </p>
<p></p>
<p> Puts will add another line character and when you call .class on both puts and print method it will return Nilclass</p>
<p></p>
<p> def greeting                                </p>
<p> 	puts "Hello"</p>
<p> end</p>
<p> greeting # => call the method</p>
<p> Hello</p>
<p>=> nil # =>extra line character</p>
<p>greeting.class => NilClass</p>
<p></p>
<p>def greeting</p>
<p>   print "Hello"</p>
<p>end</p>
<p>greeting # => call the method</p>
<p>Hello=> nil #=> no extra line character</p>
<p>greeting.class  # => NilClass </p>
<p></p>
<p>In the following example I used return but with Ruby you can also do it without return if its the last line of code . I called the .class method and it returned String Class</p>
<p></p>
<p>def greeting</p>
<p> return "Hello"</p>
<p>end</p>
<p>greeting</p>
<p>“Hello”</p>
<p>greeting.class  => String</p>
<p></p>
<p>A good example of not to use puts and prints for return value </p>
<p> def sum  </p>
<p>    x = 2 + 5</p>
<p>    puts x</p>
<p>end</p>
<p>y = 7</p>
<p>sum + y </p>
<p>You  will get NoMethodError( undefined method ‘+’ for nil:NilClass)</p>
<p>If you remove Puts you will get the desired result of </p>
<p>sum + y => 14.</p>
<p>We can use p which is similar to .inspect which is good for debugging </p>
<p></p>
<p>p “foo”</p>
<p>“foo” # output to user</p>
<p>=> “foo” #=> return value String </p>
<p></p>
<p></p>
</div>
