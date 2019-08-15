---
layout: post
title: Alexa Magic Card Skill
thumbnail-path: "img/amazon_alexa.jpg"
short-description: Making use of Amazon Web Services, this Skill lets the user say the name of any Magic Card from Khans of Tarkir block onwards, and retrieve all printed information about that card.
---

{:.center}
![]({{site.baseurl}}/img/mtg-logo.png)

## Summary

The Alexa Magic Card Skill allows users to say the name of any Magic card printed from the Theros block all the way up to Aether Revolt. For those unfamiliar, <a href="http://magic.wizards.com/en">Magic the Gathering</a> is a trading card game that has grown in popularity since 1993. The Alexa Skill can recognize several thousand different cards.
## Explanation

As part of my development with the Bloc curriculum, I was tasked with choosing two of my own specialization projects. Developing an app for Amazon's Alexa platform seemed like a great challenge that also had practical implications. Coding anything from a board game to a consumer-focused voice-controlled program serves to increase both my confidence and breadth of experience as a developer.

## Problem

The problem statement for my assignment was "Develop an Alexa Skill." I appreciated this wide scope; it allowed me to create an app that was personally interesting. 

Figuring out how to actually work with Alexa was another challenge. Amazon's documentation is quite comprehensive, which is a doubled-edged sword. With so much information to get through, it took a bit of time to learn how to leverage the power of the app.

I chose to make an app that had to recognize mystical proper nouns. Common titles for Magic Cards include things like "Entomber Exarch", "Golgari Guildgate", and "Zur the Enchanter". Even for an advanced voice recognition like Alexa, one can imagine the difficulty in accurately recognizing such phrases.

## Solutions

My initial intention was to create an Alexa Skill that let the user say the name of any large company, and Alexa would relay information about that company's current stock price, and allow the option to ask for historical pricing trends. Of course, this would require finding some (ideally free) API that ties into some database that updates in at least near-real-time. It was surprisingly hard to find such an API that didn't require approvals or subscriptions, or payment. But, as I mention in <a href="http://andrewmbyrd.github.io/2017/02/13/alexa-cards.html">my blog post about the subject</a>, the process for obtaining information about a Magic Card is largely similar; use an API to get at a database of cards, and the user will be able to hear information abou them. I used the API located <a href="https://docs.magicthegathering.io/#overview">here</a> to access the cards.

Actually learning the innards of Alexa was an interesting process. Amazon graciously provides <a href="https://github.com/alexa">several example Skills</a> to walk new devlopers through the process of getting a new skill up and running. I refer the reader to my <a href="http://andrewmbyrd.github.io/2017/02/01/alexa.html">blog post</a> about discovering how to work Alexa. 

The database I used for getting at Magic Card information was impressively maintained. In order to leverage the full power of the database, my greatest hurdle was in familiarizing myself with syntax in Ecma Script, and getting to understand the Promises in Node.js. The module <a href="https://github.com/workshopper/learnyounode">learnyounode</a> was a great tool for getting started with promises.

The promise is a key piece in asynchronous programming. The benefit of asynchronous programming is that an operation that takes a long time to complete doesn't hold up other processes from running. The best analogy I read was a comparison to a fast food restaraunt. If a customer ordered her food and then no one else behind her in line could order until her food was prepared, that would be synchronous programming. With asynchronous programming, the customer can order his food, go sit down and wait for it, and all the other customers can proceed on to do the same.

The callback notation of regular Javascript can be quite confusing:

{% highlight javascript %}
function(x, y, z, function(a,b,c){
            //do something
}){
//do something
}

{% endhighlight %}

Which is why I like ecma script's `.then` notation:

{% highlight javascript %}
retrieveCardByName(intent.slots.card.value).then(function(card){
        if (card && session.attributes.wantsToChangeCards){
            session.attributes.currentCardObject = card;
            var speechOutput = {
                speech: card.name + "'s mana cost is " + updateManaCost(card.manaCost) + ", type is " + card.type + ".. card text is " + updateManaCost(card.text) + " ...You can say a different card now if you'd like. Otherwise: would you like to hear more details about this card?" ,
                type: AlexaSkill.speechOutputType.PLAIN_TEXT
            };
{% endhighlight %}


## Results

The skill can quite reliably recognize even the most obscure card names. As I alluded to in my blog post above, the optimal solution seemed to be to just tell Alexa thousands of card names that she should expect to hear. While this seems less futuristic than a Watson-style language interpreting AI, the end user experience of just saying the name of a card and then hearing all the information about it is still quite special.

## Conclusion

The Skill is currently under review by the Alexa Skills team. I will post a link to it when it is approved.



     

































