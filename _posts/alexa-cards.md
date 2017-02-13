---
layout: post
title: Building an Alexa Skill to report Stock Prices
---

After having given a shot a querying real-time stock information, I decided to go ahead and look up Magic Cards instead. Finding a free, easy-to-use, readily available API for getting at stock prices proved harder than I thought it would (or should) be. I thought it wouldn't really matter; the process for getting at the information is exactly the same - name a thing, have the program look at a database to find that thing, and then tell you information about the thing.

But the problem is indeed in naming the thing. Alexa wants you to set up custom slots in which you tell her what kinds of things she should expect to hear in your app. With looking up Magic cards, there are two distinct things you need to be able to say: card names, and card attributes. With that in mind, I set two custom intents, each with a list of sample Utterances which would indicate a reference to that intent.

Now there is a huge asymmetry here. There are only about two dozen card attributes that exist. They are all standard English words like "power", "rarity", "set name", "mana cost".

By the way, here's what a Magic card looks like in case you're not familiar. It's explained in further detail <a href="http://magic.wizards.com/en/game-info/planeswalker-cards"> here </a>

{:.center}
![NTDOY stock prices]({{ site.baseurl }}/img/stock_price.PNG)

On the other hand, there are thousands and tens of thousands of _names_ of cards. Further, the names are the opposite of standard words you'd find in an English dictionary. 

With that in mind, I decided to try to help Alexa as best I could by telling her every card _attribute_ that she could expect to hear, in the hopes that if she didn't hear any of those couple-dozen words, then she would know that it wasn't an _attribute_ that she was hearing, but a _name_. In testing, I found that even when none of the list of ~19 attributes I gave her was said, she still usually assumed that whatever I said to her was a _GetCardAttributeIntent_. I tried to help this by using the AMAZON.LITERAL Intent, which ostensibly restricts her understanding to explicitly the word you say in the sample Utterances (i.e. she doesn't try to generalize based on those words), but that didn't work.

The final solution came down to actually importing a list of several thousand card names. That greatly increased Alexa's ability to understand a name when she heard it, although she still has problems with punctuation on occasion.

But the app is now deployed and awaiting certification from Amazon. You can search "Magic Cards" to find it. For those who would have interest: Alexa should be able to understand quite well any card from Theros block all the way up to Aether Revolt.
