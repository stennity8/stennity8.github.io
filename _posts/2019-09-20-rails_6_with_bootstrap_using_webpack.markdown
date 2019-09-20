---
layout: post
title:      "Rails 6 with Bootstrap using Webpack"
date:       2019-09-20 14:31:03 -0400
permalink:  rails_6_with_bootstrap_using_webpack
---


I am a fan of Boostrap and have used it several times.  For my Rails project I played around with Materialize during my initial implementation but decided to go back to Bootstrap.  This was my first project in Rails and I knew very little about how JavaScript worked within the Rails ecosystem.  I debated whether I should just use the Bootstrap CDN's in my project or try to implement them directly through the Rails asset pipeline.  I decided to go the asset pipeline route as my Flatiron Projects are a chance to learn some new things while solidifying the course work.

Well as it turns out Rails 6 has completely changed the asset pipeline for JavaScript and I had officially gone down a rabbit hole.  Luckily I found a video on the GoRails YouTube channel, http://https://www.youtube.com/watch?v=bn9arlhfaXc.   The video walked through the steps to set up Boostrap using the new Rails 6 way of doing Javascript, which uses Webpacker.  The summary of those steps are:

1.   Run `yarn add bootstrap jquery popper.js`
2.   Navigate to the config/webpack/environment.js file and add update it to look like this:  > const {  environment } = require('@rails/webpacker')
> 
> const webpack = require('webpack')
> environment.plugins.append(
> 'Provide',
> new webpack.ProvidePlugin({
>  $: 'jquery', jQuery: 'jquery',
> Popper: ['popper.js', 'default']
> })
> )
>  module.exports = environment  

3.  Navigate to app/javascript/pack/application.js and add update to look like the following: 
> require("@rails/ujs").start()
> require("turbolinks").start()
> require("@rails/activestorage").start()
> require("channels")
> 
> import "bootstrap"
> import "../stylesheets/application"
> 
> document.addEventListener("turbolinks:load", () => {
> $('[data-toggle="tooltip"]').tooltip()
> $('[data-toggle="popover"]').popover()
> })
4.   Navigate to the app/javascript/stylesheets/application.scss and add the following to the top:   `@import "~bootstrap/scss/bootstrap";`
5.  The last step is to make sure that your layout/application.html.erb has all three of the following the <head> tag:
>   <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
>   <%= stylesheet_pack_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
>   <%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %> 
>   

You can now add your HTML and should have access to all the Bootsrap classes and features!


