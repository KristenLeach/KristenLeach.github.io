---
layout: post
title:      "Using Async-Await in Javascript"
date:       2018-10-09 18:52:26 +0000
permalink:  using_async-await_in_javascript
---

https://medium.com/@kristenleach24/using-async-await-in-javascript-926f1b2766e4

Promises are powerful. I mean, in real life too, but I am talking about in code. To understand why promises are so great, we need to understand how Javascript works.

Javascript is a threaded language. That means it can only accomplish one thing at a time. Sometimes we can use events to handle this issue, but that can give us problems too. Say you set a click event on a link, but what if that click event listener has not yet triggered when a user clicks on the link? This is where promises can come in handy. A promise is an object that may produce a value in the future. We see this a lot in code; take fetch requests for example. A fetch request will always return a promise object. Why? Sending an HTTP request can take time. If you sent a request to an API on one line and tried converting it to JSON immediately, it would fail. This is because that JSON line of code would be hit *before* the GET request completed. You’d be trying to convert data to JSON when you don’t even have that data yet! Thus, promises. Typically, promises are used with the .then() method, which does just what it says. After the request resolves, THEN convert to JSON, etc. But we’ve got a new way of handling promises (and even creating promises from non-promise code. Whaahhh?!)

Async-Await! The easiest way to explain it is to show how it works. Let’s say we have a function retrieveCats() that gets pictures of cats from an API. After that API is hit, we want to convert to JSON and then console.log those JSON results. This is what that would look like if we were using regular promises and that then() function:


I mean, it’s not bad. But let’s see that with async-await:


Isn’t it just… cleaner? So let’s take a look at what is happening here. The first rule of async-await is you MUST have “async” before the function in order to use await. Await CANNOT be used alone. Async returns a promise, so even if you wrap a function that contains something like “return “Hello World!” using async will wrap that return value in a resolved promise. Pretty cool, right? That means you can use async-await to make your asynchronous code appear to run more synchronously. The await keyword, much like the then() function, tells the code to await the value of what is being passed to it. So in the code snippet above, “cats” is actually equal to the RESOLVED value of retrieveCats(), not just the promise of a future value of that HTTP request. Similarly, ‘catsJSON’ is equal to the JSON value of the cats object, as it awaits that promise to be resolved before continuing on to the console.log. If we didn’t have these promise handlers in here, console.log would be hit before cats and catsJSON were resolved, and catsJSON would be undefined.

Another cool thing about async-await is that it allows you to chain on those then() functions as well. Async-await isn’t always right for every situation, but you can blend regular promise handling with it to get the best timing and outcome for your program. It may take some practice to get the hang of it, but async-await is a great way to implement promise handling inside of your program!
