---
layout: post
title: Blocipedia
thumbnail-path: "img/wiki_list.png"
short-description: Blocipedia is a Ruby on Rails-powered posting site, where users can create and update wiki entries.

---

{:.center}
![]({{site.baseurl}}/img/wiki_list.png)

## Summary

Blocipedia is a system not unlike any other wiki hosting site. Users can upload posts, add comments and even create private wikis for collaboration by enrolling in a premium membership. You can visit the app and play around in it for yourself, <a href="https://secret-cove-26230.herokuapp.com/users/sign_in">here</a>.

## Explanation

Understanding how to implement a wide variety of programming languages and frameworks is an important skill for any software developer. Blocipedia is my demonstration of command over Ruby on Rails. After having been guided through a Rails-powered Reddit clone in the Bloc curriculum, I was tasked with creating my own project. Blocipedia shows all of the characteristics of a Rails application, including data persistence, routing, partials, html.erb files and more.

## Points of Interest

This project takes advantage of the Ruby on Rails platform to deliver an app backed by CRUD storage. The great thing about Ruby and Rails is that there is so much functionality that is either built in to Rails, or can be imported in with Ruby Gems. A simple `rails g` puts in the scaffolding for everything you need to have your app up and running. I suppose this is why they call it "on Rails" because you're bound by the "tracks" of the framework, but they can get you where you're going with great speed.

The CSS/SASS styling was all handled by a pre-existing template. Log in information is controlled by the `devise` gem. A great deal of creating a useful Ruby app is leveraging existing code for your own benefit.

The app has the capability to integrate with Stripe. There is a stripe gem, and the API makes it easy to "plug and play" in your app. By signing up for a premium membership, the user is able to create private wikis and add collaborators to those private wikis.

{:.center}
![]({{site.baseurl}}/img/stripe_premium.png)

By maintaining a `session` object, the app can display the appropriate amount of information to the user, depending on his or her status. Any private wikis are not displayed to non-authorized users and even the buttons to create topics and make edits won't appear unless the session user is authorized to do so.

As a side note, the development process was made _vastly_ easier when I realized that while your bash is maintaining a local server using `rails s`, everytime you engage a different route in your app, a nice hash shows exactly what `params` is at that time! Somehow this wasn't advertised at the top of the documentations! But this made it much easier to ensure that user status and other session info was being tracked correctly.

The last nice feature is that this app employs the somewhat complex `has many through` relationship to relate Users to Wikis that they didn't create _through_ a collaborators table. The actual implications of this became more clear to me as I created my own ORM, which you can find on my github page <a href="https://github.com/andrewmbyrd/databases">here</a>

## Results

The result is a fully functional data-persisting website that enforces user authentication, connects with third-party payment services, and maintains relationships between database tables. 

## Conclusion

Rails is a very powerful framework that allows for apps to be deployed quickly, becuase the skeleton of most of what you want to do is provided for you. External Gems make life even easier by providing functionality that could take days or weeks to code otherwise. Being able to leverage these tools allows for efficient creation of professional-level tools.
