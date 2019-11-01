---
layout: post
title:      "`this` is Interesting"
date:       2019-11-01 18:44:49 +0000
permalink:  this_is_interesting
---

As I was working through my JavaScript with Rail API project I found myself struggling with `this`.  While I could make things work by using `.bind(this)` I felt like my code was starting to get ugly with all those `.bind(this)` scattered everywhere.  I knew I could use `=>` functions to avoid this but the few attempts I made with them I could not get them to work.

Luckily I had a scheduled trip to Philly for a friends engagement party.  Why is that lucky?  Well my friend who's engagement party it was is a very experienced JS developer and has been mentoring me throughout this career transition.  We hadn't had a chance to talk in a little over a month so I had a lot of questions for him.  But the most important one was about `this`.  

I showed him my code and explained how I could get things to work with `.bind(this)` and but could not seem to get it to work with `=>` functions.  It should be noted this was in the context of eventListeners.  He explained that with the `.bind(this)` you are binding the `this` to the function but you do not call the function.  
`issueContainer.querySelector('.close-view').addEventListener('click', this.closeView.bind(this))`

Which I understood.  But when using the `=>` function you actually need to write the function to look like it would if you were invoking right then.
`document.querySelector('.close-view').addEventListener('click', (event) => this.closeView(event))`

While they do essentially the same thing the `=>` is more elegant and was specifically developed for this situation. 
