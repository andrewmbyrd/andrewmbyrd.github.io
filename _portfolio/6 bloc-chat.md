---
layout: post
title: Bloc Chat
thumbnail-path: "img/bloc_chat.JPG"
short-description: Bloc Chat is a Google Firebase-driven chat application in which users can create message boards and post messages within.

---

{:.center}
![]({{site.baseurl}}/img/bloc_chat.JPG)

## Summary

Bloc chat is a simple chat site that allows user to create chat rooms and write posts. Chat rooms and messages are persisted by leveraging Google's Firebase database. You can visit the app <a href="https://stormy-lake-42590.herokuapp.com/">here</a>.
## Explanation

Bloc chat maintains a special place in coding history (lol) by being the first application that I developed without any strong guidance. After having just learned how AngularJS is structured with the previous project, the Bloc curriculum tasked me with creating this project using the AngularJS framework.


## Talking points

As one can see by the simple UI, this application was built from the ground up by a programmer who had a few weeks of experience. I've elected not to update the visuals as a reminder of how far I've come (and am going) in my software development career. 

Laying out everything just how I wanted it was a nice experience. I, by no means, think of myself as a great UI designer. I think I'm much better suited at implementing functionality than designing something that is nice to look at. For this reason, using ready-made css packages in my more recent work has proven beneficial.

The most frustrating part of the project was working with modals. Apparently everyone hates those, and for good reason! When I imported the library to help generate the modal, I knew I had followed all of the instructions clearly to get it to display properly. Turns out, it was appearing _below_ all of my other content. There is a css `z-index` property that I had to adjust to an arbitratily high number to be able to actually see the modal on the screen.

Other than that, working with Google's firebase database was quite straightforward. Being able to log into the firebase console and see the messages appear in real time is a great help.
## Results

This very simple app will take in strings and output them on the screen for others with access to the database to see. For a first project, I'm actually quite proud of it, because it requrired an understanding of the AngularJS framework, fundamental HTML and CSS, and tying into specialized functionalities like modals and Google's Firebase.

## Conclusion

While not the fanciest piece of software ever developed, Bloc Chat is a perfectly functional chat room. You can try out some of your own messages <a href="https://stormy-lake-42590.herokuapp.com/">here</a>.


     

































