---
layout: post
title: BlocJams
thumbnail-path: "img/blocjams.png"
short-description: BlocJams is a web-based music player that can display a collection of albums and play songs from you browser.

---

{:.center}
![]({{site.baseurl}}/img/blocjams.png)

## Summary

There are no web-based music players that can handle great works from the likes of Pablo Picasso. Bloc Jams was created to faciliate easy music streaming from your favorite browser, on your home computer or mobile device. This fully functional player lets you store and view your collection of albums, plays songs, even control *volume*.

## Explanation

Bloc needed something to show off what they could do; they had to prove they had the right curriculum to deliver great web developers to top companies. They needed their students to be able to deliver a practical project that was fair, challenging, and fun. Students needed to gain confidence and programming experience within only a few weeks. This was the environment which gave rise to BlocJams. For this round, I was the student - the junior developer that would prove to the world that BlocJams could be done by someone with no html, css, or javascript experience whatsoever.

## Problem

When I was shown the framework that had been built for BlocJams, the application was only half complete. The Bloc team needed me to improve functionality in several ways:

1. After a user was in the view page for an album, there was no way to get to another album without first having to
⋅⋅* Click out of the current album
⋅⋅* Find the next album to be played and click on it
This was clunky and undesireable.

2. There was non-DRY code in the change song functionality. The Next and Previous song buttons each had their own function definitions, even though they perform almost identically.

3. The time that the song had been playing was not updating correctly. Users could not search to their favorite part of any song

## Solutions

* The team did not know how to loop through available albums, so I was hired on to find a way to connect each album sequentially, without the need to go back to the general album collection page.

The first requirement was to find a way to link all of the albums together. I chose to use an array in which every album object was immediately followed by its album Artist.
{% highlight javascript %}
//create a list of all the currently available albums and their artists
+var albums=[albumPicasso,"Pablo Picasso",albumMarconi,"Guglielmo Marconi",albumKong,"David Wise"];
{% endhighlight %}

After having collated the albums in such a way, it was then possible to ensure a standard rotation of albums upon a click event by grabbing the index of the the artist name of the album which had been clicked. This name was stored as a node in the page.

{% highlight javascript %}
//find the index of the current album object, and loop through to the next one (or first if at end)
var index=albums.indexOf(document.getElementsByClassName("album-view-artist")[0].innerHTML);
	if(index'<'albums.length){
	setCurrentAlbum(albums[index+1]);
      }
{%endhighlight%}

* The website had slow performance due to inefficient code. The next/forward buttons on the music player each had their own individual functions. I was able to reduce the lines of code by refactoring those two functions into one.

The key was in realizing that previous and next functions do exactly the same thing - except which direction in the list of songs you go. The key big of code was in identifying the class of the element that receive the click event

{% highlight javascript %}

//check if the button that was clicked was the Forward button. if it was, increment the //currentlyPlayingSong number, or loop to the beginning if it was at the end 
if(event.target.className==="ion-skip-forward"){ 
  //set the song number to the next song. if we're at the end of the list, loop around 
  if (trackIndex(currentAlbum,currentSongFromAlbum)===currentAlbum.songs.length-1 ){
      
      currentlyPlayingSongNumber=1;
  }else{
      
      currentlyPlayingSongNumber++;
  
{% endhighlight %}

* Finally, I was able to invoke Math functions in order to update current playing time in a song, and to correct the html in real-time to reflect those changes accordingly.

## Results

One of the best thing about this job was the ease of testing. They say all children are born with a scientific mind: create a hypothesis, test it, observe results, repeat. This process was made easy with the tool <a href="http://brackets.io/">Brackets</a>. Testing was performed in real-time to ensure that the code implemented was successful.

## Conclusion

Each of these solutions I've presented here worked, but that doesn't mean there weren't road bumps along the way. The biggest problem was getting the syntax of JavaScript and CSS and HTML fully under control. A good deal of time was spent correcting, not logic issues, but essentially grammatical errors. 

The most surprising aspect of the project was the degree to which one has to understand the entire scope of a program or application in order to create a fix for one part without breaking another. During this project I learned to use jQuery, DOM elements and event listeners. I'll use that knowledge to build more projects!

     

































