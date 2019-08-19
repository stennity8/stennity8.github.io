---
layout: post
title:      "Freezing and Pre-populating Form Dropdowns"
date:       2019-08-19 18:36:45 +0000
permalink:  freezing_and_pre-populating_form_dropdowns
---


During my time working on my Sinatra project I came across some interesting issues with dropdowns in forms.  Issues may not be the right word...more like learning hiccups.  A little backstory on the application and the issue.  The app I created is a restaurant review app.  Users can both create new restaurants and review existing restaurants.  I decided to use the same form for the creation of both types of reviews.  The intention was for the user who created the restaurant to have access to edit the restaurant, while other users could see the restaurant details but not edit the restaurant.  

The first issue that arose was with pre-populating my form.  I had chosen to use drop downs for both the "Cuisine" and "State" inputs of my form.  I tried to set the `value` equal to the existing value like you can do for text inputs but this did not work.  What I found out is you can not preset a drop down this way.  This is because each option in a drop down has it's own `<option>` tag.  In order to preselect it you need to imbed `selected` within the `<option>` tag that you would like pre-populated.  I did find a few solutions using JavaScript but I decided to use an array and iterate over the array.  I created an array within my `.erb` file of all the available options the user can select, looped over each option and compared it to the objects value.  The iteration would then put `selected` within the correct tag and add nothing additional for all the other options.  Form issue #1 out of the way. 

The next issue was freezing the form inputs when the user was not the creator of the restaurant and therefore should not have access to edit the restaurant.  My intention was to use the `read only` functionality that can be added to the `input` HTML tag on all the tags.  So I created helper function to insert `read only` into the `<input>` tags based on whether the user created the restaurant.  This however, did not work for the dropdowns.  Turns out, dropdowns actually require you use `disabled` and not `read-only`.  So I created a helper function for `disabled` as well and it worked.

Those were just a couple of hiccups on this project but as usual each hiccup leads to more knowledge.
