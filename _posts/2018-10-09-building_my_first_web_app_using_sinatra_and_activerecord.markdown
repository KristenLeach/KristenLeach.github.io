---
layout: post
title:      "Building my first web app using Sinatra & ActiveRecord"
date:       2018-10-09 18:46:45 +0000
permalink:  building_my_first_web_app_using_sinatra_and_activerecord
---

Working through labs in a web development course can be really challenging. The tests used to check whether your program is working as expected are often written in very specific terms. Failing a test doesn’t necessarily mean that your code doesn’t work, sometimes it just means the tests are looking for something that works the same way but is written differently. Regardless, struggling through lab tests like this can make you feel as though you are severely lacking the information you need to be a web developer; it can be discouraging. My most recent portfolio project helped me to see this effect from a different perspective.

After struggling through a couple of really intricate MVC labs at Flatiron School, it was time to start my portfolio project for Sinatra and build a web app from scratch. Before starting this project, I would break out in a cold sweat. I struggled to get through those labs beforehand, I had no idea if I had the tools and understanding I needed to do this project. After brainstorming (er… procrastinating) for a few days, I finally got to work.

I went through several ideas of what kind of app to build before settled on building a knitting project app. First, I built my models. I knew I needed a user and a project; a user would have many projects, and a project belongs to the user. I wrote validations for the user, to be sure that a new user could not be created without an email address, username, and password. Thanks to ActiveRecord, that is really all that went into the model portion of my web application.

The database was next. The user table needed a username, an email, and a password that is encrypted using the ruby gem bcrypt. The project table originally had a name, instructions, and materials. I later returned and added an image URL to the database, as it seemed fitting for the kind of user interaction I was looking for.

Building the controllers and views was a little more complicated. I started with my controller; I would build the route to a page, like the login page, for example, and then build the view. Once the form was finished in the view, I went back to the controller to build the post method that took the in the params to build the actual objects. The back and forth of this took extra time, but it was still very straightforward. What took the most thought in the controllers were the validation checks. Besides the validations ActiveRecord completes for us, I also needed to write many if/else statements for things like checking if someone was logged in before editing/deleting a project, if they were the owner of the project, etc.

And there we have it; the MVC portion was complete. Honestly, what took me the longest was adding CSS and organizing the HTML in the views since I haven’t used them in so long, but it just took some googling to jog my memory. What I thought would be an impossible feat turned out to be fairly straightforward thanks to the magic of ActiveRecord and Sinatra.

Knit Happens. That’s my web app. And it might not be the most intricate piece of web development ever made, but it works, and completing it without any major hangups has made me feel more confident in my abilities as a novice web developer. I’m looking forward to diving into Rails; I can’t see what dev magic lies ahead.


