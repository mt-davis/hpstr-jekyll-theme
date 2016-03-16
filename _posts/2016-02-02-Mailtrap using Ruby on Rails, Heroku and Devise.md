---
published: true
title: Mailtrap using Ruby on Rails, Heroku and Devise.
description: "Create a fake SMTP server for pre-production testing of an applications email functionality without the risk of spamming actually users or customers"
tags: [Ruby on Rails, Mailtrap, Heroku, Devise]
layout: post   
date: 2016-02-02 13:00:00
image:
  feature: coding.jpg
  credit: Unknown
  creditlink: http://wallpaperswide.com/programming-wallpapers.html
  background: witewall_3.png
---

In this tutorial, we'll be using Mailtrap to impliement the password reset feature in the Devise gem. Mailtrap allows developers to create a fake SMTP server for pre-production testing of an applications email functionality without the risk of spamming actually users or customers. 

We will be using Heroku to run Mailtrap for this tutorial because of the easy implementation of the Mailtrap service. However, keep in mind this will be for a development environment even thou we are using Heroku.

![Mailtrap](https://s3.amazonaws.com/github-mtdavis/mailtrap-home.jpg)

I will assume that you have a development environment setup and an account with Heroku. If not, please visit [Heroku](http://heroku.com) to setup an account now.

##Lets Get Started
If you have Devise install, you can skip this section.
Make sure you have the Devise gem in your gemfile.
`gem devise`

Run the bundle command to install it:
`bundle install`

After you install Devise and it's been added to your Gemfile, you need to run the Devise generator:
`rails generate devise:install`

Then you want to add Devise to any of your models using the generator:
`rails generate devise MODEL`

Replace "MODEL" with the model name used for the application's user. Most of the time, it's just `User` or `Admin`.

Next you need to set up the default URL option {% highlight ruby %}`config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }`{% endhighlight %} for the Devise mailer in `app\environments\development.rb` file

Lastly, you want to create the Devise views:
`rails g devise:views`

This will create the password reset, confirmation and other Devise views.

Make sure you add {% highlight ruby %} `before_action :authenticate_user!` {% endhighlight %} to the controller that you want to associate user authentication too.

Also make sure that {% highlight ruby %}`config.sign_out_via = :get`{% endhighlight %} is set correctly in `app\config\initializers\devise.rb`. This is the default HTTP method used to sign out a resource. The default is `:delete`. Be sure to restart your rails server with `rails s`.

##Optional 
To display the alerts after requesting the password reset, adding the following code to `app\layouts\application.html.erb` <br> 
{% highlight erb %}
<p class="notice"><%= notice %></p>
<p class="alert"><%= alert %></p>
{% endhighlight %}
<br>
place it in between the `<body>` and `<%= yield%>` tags.

##Setting up Mailtrap on Heroku
We will skip deploying an app on Heroku. You can visit [Heroku App Deployment](https://devcenter.heroku.com/articles/git) to get directions on that. Once you have your app setup, you want to enter this following in the CLI: 
`heroku addons:create mailtrap` This will atttached Mailtrap to your Heroku application.

Next, navigate to your Heroku dashboard and select your app and then Mailtrap by Railsware add on.

![Heroku Dashboard](https://s3.amazonaws.com/github-mtdavis/heroku-db.JPG)


This will bring you to the Mailtrap Dashboard:

![Mailtrap Dashboard](https://s3.amazonaws.com/github-mtdavis/mailtrap-dash.JPG)

Then click on "Demo Inbox"

You will see your credentials. You want to copy and past the code for Ruby on Rails. It should look something like this:

{% highlight ruby %}
config.action_mailer.delivery_method = :smtp
config.action_mailer.smtp_settings = {
  :user_name => '748a0f58237051',
  :password => '82612e24f66a8e',
  :address => 'mailtrap.io',
  :domain => 'mailtrap.io',
  :port => '2525',
  :authentication => :cram_md5
}
{% endhighlight %}

You want to place this in your `app\config\environments\development.rb` file. Make sure that you have {% highlight ruby %}`config.action_mailer.perform_deliveries = true`{% endhighlight %} in that file as well. Once you have everything setup, you should be able to to reset your password at http://localhost:3000/users/sign_in and click on "Forgot your password?" then go back to the Mailtrap dasboard and see your test email.

##In Conclusion
Mailtrap is an easy and quick solution to test email functionality without having to install and configure your own SMTP server. Mailtrap supports the following lanaguages and framworks:

* Ruby on Rails
* PHP (Most Frameworks)
* Python (Django)
* Node.Js (Nodemailer)
* Java, Scala
* Perl (MIME::Lite)
* C# (Plain C#)

You can setup and share multiple test inboxes for teams within your company. Check out [Mailtrap](https://mailtrap.io/pricing) for more information.

There is a lot more that you can do with Mailtrap. I just wanted to show how to get it up and running with the service using Heroku in a development environment. Please add any comments below.