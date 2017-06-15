---
layout: post
title: disPlay
thumbnail-path: "img/disPlay.png"
short-description: disPlay is the essential tool for digitally showing off your collection of games across all platforms.

---

{:.center}
[![disPlay]({{site.baseurl}}/img/disPlay_home.JPG)](https://secure-stream-70012.herokuapp.com)

## Summary

As digital downloads become more prominent in the gaming world, it is becoming harder to capture the classic feeling of showing off your library of games. Rather than trying to fight this trend, disPlay embraces it, creating a virtual haven for all of your content. Users can proudly display their games on their Library shelves, review content, and follow other users who are doing the same. With this focus on community, users can flaunt their favorite games, and discover their new favorite franchise through the recommendations of their friends.

## Explanation

The app is built with Ruby on Rails. For this application, Rails' data persistence, routing, and gem availability make it an ideal choice for implementation. I've enjoyed liberal use of the [devise gem](https://github.com/plataformatec/devise), [bootstrap css](http://getbootstrap.com/css/), [fuzzymatch](https://github.com/seamusabshere/fuzzy_match), and [gravatar](https://en.gravatar.com/) in order to make the app function in the way it does.

In order to get at the actual data I needed for this specific app, I built [my own API wrapper](https://github.com/andrewmbyrd/giant-bomber) for [Giant Bomb's](https://www.giantbomb.com/api/documentation) game database API. The source database isn't perfect, but it has been a great help in providing the raw data I needed for the app.

The rest of the data is contained in the tables shown here:

{:.center}
![disPlay databases]({{site.baseurl}}/img/databases.JPG)

The relationships between those databases are shown here:

![disPlay relationships]({{site.baseurl}}/img/relationships.jpg)

If that looks complex, that's because it is. The blue lines represent a BelongsTo relationship (implying a HasOne or HasMany relationship on the recipient of the arrow head). The red curves denote a HasManyThrough relationship, where the `:through` is the table encircled by the red curves. Fortunately, Rails provides robust methods for allowing each of these databases to talk to one another, as well has SQL translations for creating join tables, getting averages of a certain property, etc. I've used database queries wherever applicable to ensure that the app can still be performant as it scales.

## Future Steps

The next phase of improvement for this app will be in procuring a more robust, accurate database of games. The app can update at scheduled intervals, during periods of low historical usage in order to maintain pace with all of the latest releases of games. The slowest part of the app right now is in making web requests to fetch the cover art for each of the games for any particular system. This problem can be alleviated by storing the images locally in a wishfully perfect database, rather than fetching them from another website.

In the ideal case, companies will recognize that this is free advertising for their games, so they would be on board to integrate automatic updating of `Game Purchases` in disPlay with real-life game purchases. The average user greatly benefits as well, because they can look at reviews of their friends, YouTube personalities, popular Tweeters, etc. in order to make purchasing decisions based on the opinions of people whom they trust. And of course, their is an intangible value in having a single, curated place to show off all of one's digital and physical content

## References

The live app can be found [here](https://secure-stream-70012.herokuapp.com). Source code is located on [my github page](https://github.com/andrewmbyrd/disPlay)














