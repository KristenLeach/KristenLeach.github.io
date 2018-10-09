---
layout: post
title:      "Overthinking and Persevering: Building My First Ruby Gem"
date:       2018-10-09 18:46:08 +0000
permalink:  overthinking_and_persevering_building_my_first_ruby_gem
---

I had been dreading this project for weeks. Perhaps that was where my problems began? Who knows. All I know for sure is that the break over Christmas made me feel like I was a ‘Ruby Newbie’ all over again, and yet I was slated to begin my final project within a couple of weeks of getting back to work. I was stressing. Seriously stressing. And while it wasn’t AS bad as I was expecting, I certainly ran into some hurtles.

I began with a pretty solid idea; I knew I wanted to scrape a website for books. I knew I wanted to go three levels deep; categories, bestsellers, and descriptions of individual books. My first mistake was choosing a website that looked like it hadn’t been updated since the 90’s. The bookstore that shall not be named gave me headaches from the start. My first attempt to scrape their category list gave me typos, duplicate category names, and jumbled alphabetization. When I dug a bit deeper, I realized that their bestseller lists by category were actually three levels deep; making book descriptions 4 levels deep for my poor Nokogiri scraper. Yeah, not worth it. At least not when there are plenty of other bookstores on the web.

So I settled on the big one; Barnes & Noble. Overall, scraping it was relatively easy, save for the random hiccup here and there. Once the scrapers were built, I had to move on to the part I had been avoiding like the plague; how would my logic work? Would I have one object, or two? And WHERE would this book description (which had it’s own scraper for this one tiny piece of information) even go? Surely it wouldn’t need it’s own class, but how do I append onto a hash that belongs to an object that ALREADY EXISTS?

I’m sure I over thought that one, but after some trial and error I figured out how to get it working. Building my Category class was simple; I referenced a previous scraper lab that was similar. Book was just as easy; just grab the information and assign it to each book object. In order to get the description added to each book after the book was created, however, took a bit. In the end, I pushed all of the book objects into a constant within the class. That way, after the description scraper finished running I could reference the index of the book the description belonged to in the scraper class and push the value of the description onto an empty key that I created in the book object’s scraper. It made my head spin, but dammit, that was a super cool thing I didn’t know I could do. I am pretty happy with how that works; even if there are better ways of setting it up.

After that, I began working on putting it all together in my CLI. That went quite smoothly. The only major issue I ran into was the fact that once my program looped (when the user wants to look at a different category within the same session), all of the previous book objects still remained in existence. The more categories were called, the more unnecessary books were returned. I tried clearing the constant within the Book class, but it was still returning old books. It took me crashing a study group (and a really helpful instructor) to realize I also needed to clear the array that was built within my scraper, lest it just keep pushing the same information to the Book constant each time it ran.

The icing on my cake though- on the day I was finishing this gem, in the final hours of editing my CLI, Barnes & Noble decided to edit some of their pages. Can’t make this stuff up, folks. Bestselling lists from certain categories that I had seen moments ago were suddenly gone. Such is life. After looking at both pages that I knew had disappeared and realizing one looked like a glitch (it’s new bestselling ‘books’ included a children’s easel and an apron) and the other held different code than the bootstrap I had originally scraped, I decided to throw in the towel. It’s been two weeks. I should have used fixtures. I didn’t. I’m tired. Hopefully their Arts & Crafts page will be fixed soon for all the poor crafty souls that attempt to use my gem; regardless I will keep editing the scraper in the future.

Either way, my gem is PUBLISHED!

I am really proud of the work I did for this project. I even colorized and added some ASCII illustrations to make it look cute. I mean, why not? Ruby, though at times makes my blood boil and my brain backfire, is truly a beautiful language. Seeing my CLI app built in it’s entirety is like seeing a book that I wrote come to life. I’m looking forward for many more projects (headaches and all) to come.

Check out the Bookworm_Buddy in the video below!

https://www.useloom.com/share/8c9d43ad374e4030a45c7ccd527e9243
