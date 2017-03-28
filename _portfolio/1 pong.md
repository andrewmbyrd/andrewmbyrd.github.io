---
layout: post
title: Pong
thumbnail-path: "img/pong_portfolio_pic.JPG"
short-description: Classic Pong gameplay, with both single player and multiplayer modes. Keyboard controls and mouse control is supported! Powered by the HTML5 canvas element.

---

{:.center}
<a href="[https://evening-temple-10291.herokuapp.com/]">![pong image]({{site.baseurl}}/img/pong_welcome.JPG)</a>

## Summary
Pong is the quintessential classic gaming experience. Originally release in 1972, this game has seen countless renditions and even improvements, yet nothing can ever really stand up to the original masterpiece. My immitation of Pong allows for single and multi-player experiences, as well as multiple controls options. You can play the game <a href="https://evening-temple-10291.herokuapp.com/">here</a>!

## Explanation

As part of Bloc's curriculum, students are tasked with choosing at least 2 specialization projects. Being the avid fan of gaming that I am, it was a no-brainer for me to make my own attempt at the classic game in order to further specialize in my dream field of game development. The thing that set this project apart is that with most Bloc projects, there is at least some instruction on how to go about creating it. With this project, the instruction set was essentially, "1) Google the HTML5 canvas element. 2) Make Pong". With that, I set out to make the game. 

## Problems

The devlopment process of my first game was an interesting one. Unlike most other web applications, where items on the page are mainly static, Pong (and most other games) have their elements constantly in motion. This requires the frame to be refreshed at some frequency. The ideal here is the oft-cited gaming term "60 fps". Not a problem at all with a game as visually simplistic as Pong, but a new hurdle to overcome nonetheless.

The next concern was motion. There are two domains of motion to be concerned with in the game. Each of the paddles is capable of 1-dimensional motion. The more interesting case is that the ball is free to move in two dimensions. Translating that into a language that the computer could understand takes some insight.

Third was the issue of collision detection. Given a ball that can move in 2-D space, it is imperative to have it react realistically when it collides with either a paddle or the walls.

Lastly, any modern rendition of the game must be complete with a menu full of options. Presenting a neat, retro-flavor of menus took some insight into HTML and CSS functions, as well as external libraries.

## Solutions

In order to have the ball and paddles appear to move realistically, I needed to have a way to draw them consistently. The introduction of HTML5's <a href="http://diveintohtml5.info/canvas.html">canvas element</a> makes this convenient to execute on the browser. It takes quite a bit of code to draw elements; each line needs a start and end point, each ellipse needs a position and radius. Drawing one paddle, one time takes this much code to do:

{% highlight javascript %}
this.render = function(){
        //get the canvas element and context

        var context = canvas.getContext("2d");

        context.beginPath();

        //change this depending if I ever implement different color paddles
        context.strokeStyle = this.color;


        context.moveTo(this.x, this.y);
        context.lineWidth = this.width;
        context.lineTo(this.x, this.y + this.height);

        context.closePath();
        context.stroke();

    };
{% endhighlight %}

But that needs to be done 60 times. Every second. Fortunately, HTML5 also has a convenient <a href="https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame">request animation frame</a> function. This method takes a callback function, and executes that function at 60 Hz. By including the animation function in the callback, one can ensure that the animation happens continuously:

{% highlight javascript %}
var step = function(timestamp){
    
    render();
    if(ball.canMove)
        ball.move();
    if(!player2.isHuman){
        player2.defend();
    }
    if(ball.canMove)
        animate(step);
    
};
{% endhighlight %}

Note there are times when we want the animation to stop (i.e. when a point is scored). The `ball.canMove` property tracks that for us.


So things are able to be drawn continuously, great. The next problem is _how_ to draw them. With the paddles, movement is only up or down. Depending on the play mode, each paddle is assigned an event listener for a keypress or mouse movement, which tell it to go up or down some number of pixels.

{:.center}
![]({{site.baseurl}}/img/pong.JPG)

The much more interesting problem is that of ball movement. There must be several ways to model that mathematically for the computer, but the one I found most useful was to use our old friend the Unit Circle.

{:.center}
![]({{site.baseurl}}/img/unit_circle.png)

The unit circle beautifully describes every possible direction in the 2-D plane with <a href="https://en.wikipedia.org/wiki/Radian">radians</a>, the terms with π in them in the image above. Given a direction, we can extract the horizontal and vertical components of that direction.

Given any direction angle, θ, we can describe the _horizontal_ component of that angle with cos(θ).
The vertical component of that direction is given by sin(θ).

With the horizontal and vertical components explicitly defined, you can just add the horizontal to the ball's current x position, and add the vertical to the ball's current y position (it may also be subtracted but that's all to do with the orientaion of the canvas and the fact that values of θ between π  and 2π are negative for sin(θ), but nevermind that for now). That direction can be scaled to account for different ball speeds simply by multiplying each directional component by a constant. This way the ball isn't just moving 1 pixel every time:

{% highlight javascript %}
this.x += Math.cos(this.direction) * vectorLength;
this.y -= Math.sin(this.direction) * vectorLength;
{% endhighlight %}



Now that things can move, things are sure to run into each other! One of the most important parts of any game with constant motion is to have realistic collision detection. 

With the top and bottom walls, things are relatively straightforward. The most convincing animation is to say that for any collision with a wall, we want the angle of incidence to equal the angle of refraction. All that means is that if the ball hits the wall at 30 degrees, it should leave the wall at 30 degrees. 

{:.center}
![]({{site.baseurl}}/img/reflection.png)

The task here is again made very simple by the usage of the unit circle. The reader will notice that no matter at what angle the ball strikes a horizontal surface, the angle of reflection will simply be that angle multiplied by negative 1. There is an elegance to be appreciated here.

For colliding with a vertical surface, things get a bit more complicated. First, the detection of collision here matters a lot more; the whole point of the game is that the player wants the ball to collide with their paddle. If this doesn't work, then the user experience is ruined. So there is an interconnection between the timing of moving the ball, and detecting whether it is close enough to a paddle to collide with it.

Now there is a problem because we need to see if the edge of the ball is within a convicingly small amount of pixels from the paddle to warrant changing direction if it is between the top and bottom edges of the paddle. In order to make the game more fun, the speed, that is, the number of pixels moved in every frame, of the ball increases as a rally goes on.

So we could set it that if the left edge of the ball is within 5 pixels of the paddle, then change direction according to collision rules. Now the worst case scenario here is that the ball gets to moving so fast that at step x, the edge of the ball is 6 pixels away from the paddle, but at step x+1 the horizontal component of movement for the ball is greater than 6 pixels. If this happens, the illusion of the ball colliding with the paddle is destroyed. 

{:.center}
![]({{site.baseurl}}/img/collision.png)

To account for this, I've got an extra check in the `ball.move` method that checks if the ball is a certain range away from the paddle. If it is, then the speed of the ball is throttled down for the next frame so that collision will work properly. No one seemed to notice this small change while playing the game in testing.

Another note on collision - at first, the ball colliding with the paddles followed the same reflection principle as the walls, but that wasn't very fun. In order to give the user more control over where the ball goes, the angle of reflection for the ball is determined based on where on the paddle it is struck:

{% highlight javascript %}
//give the ball a new direction in radians, anywhere from pi/3 to -(pi/3) based on where on the paddle the ball was struck
this.direction = ((player1.y+50 - this.y)/50.0)*pi/3;
{% endhighlight %}

Lastly, we have various menu options! In order to get the font to look nice and retro, I imported a webfont library from Google. Sound is handled by the excellent <a href="http://buzz.jaysalvat.com/">buzz library</a>. There are several instance variables that are changed by having event listeners on the DOM elements of the menu `<sections>` each of which is animated to slide in when all of the available options on the previous menu have been selected. This allows the player to select their control style, paddle color, and even the difficulty of the computer. 

## Results

The result is a fully-functional rendition of the classic Pong! Don't forget to play it for yourself <a href="https://evening-temple-10291.herokuapp.com/">here!</a>

## Conclusion

This is by far my favorite project to have worked on so far in my coding career. I was able to create a faithful copy of one of the most important games of all time, and I had as much fun playing it as I did making it! The fact that I was able to apply the math that I learned back in high school was actually a thrilling experience, because I got to leverage knowledge that is not necessarily the easiest thing to just look up and play with. My next great challenge would be a foray into 3-D gaming, which I'm sure involves imaginary (lateral) numbers and all kinds of other tricks.



     

































