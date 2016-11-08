---

layout: post
title: Development Challenges
feature-img: "img/inception.jpg"

---


I knew it would be a challenge before I even came into the program. I'd had some experience with coding in the past: high school AP computer science classes, a little bit of Python in college. In general, I can trace the flow of information decently well through program. It’s meant to be fairly straightforward; code executes from top to bottom, just like reading a book, right? Simple. But I knew all along that the the main problem I would have is the same beast that stumped me in high school.


#RECURSION

Why do we even need that guy? All he does is confuse everyone.  Oh sure, you can save memory allocation, thank you very much, but that means I have to think! THAT’S WHAT THE COMPUTER IS SUPPOSED TO BE DOING FOR ME. When I have one function calling another function that might be calling itself, and may not even have been declared further up the page, that’s when I about lose it. 

Even Bloc knows the confusion on this stuff can get out of hand quickly:

{:.center}
![Callback hell]({{ site.baseurl }}/img/yodawgcallbacks.jpg)

Let me give you an example. Take this “kata” from codewars:

 The purpose of this kata is to write a higher-order function which is capable of creating a function that iterates on a specified function a given number of times. This new functions takes in an argument as a seed to start the computation from.

Here’s the code they give you to begin with

{% highlight javascript %}
var createIterator = function (func, n) {
  // TODO: Write code here to return a function 
  // that executes *func*, *n* times on a supplied input
};

{% endhighlight %}

Now you may be a bright young individual and think, “alright, I have a function that takes in a function as an argument, and says to execute that argument n times, no problem. I can do that in just one or two lines of code like this”

{% highlight javascript %}
var createIterator = function (func, n) 
	{ return function(v) { 
	   for(var i = 0; i '<' n; i++) 
	   v = func(v); 
	return v; 
}; 

};

{% endhighlight %}

And of course that would work. You just return a function that takes in a new argument, and then set the argument equal to the processing of said argument… yeah, what??? Here’s what I did:

{% highlight javascript %}
andrewmbyrd
var createIterator = function (func, n) {
  // TODO: Write code here to return a function 
  
  return function(test){
  var value=0;
  var count=0;
  if(n==1){
  return func(test);
  }
  if (n==2){
  return func(func(test));
 } 
  if (n===3){
   return func(func(func(test)));
  }
  
 }
};

{% endhighlight %}


I mean, I get what I’m trying to do, and hard coding here works, but that is BAD. I need to work on stepping back, visualizing what the program is _doing_ rather than how the program _reads_, and I think that will get me on the right track to be able to decipher this stuff better.



