---
layout: post
title:      "How and When to use BindActionCreators"
date:       2018-10-09 18:51:46 +0000
permalink:  how_and_when_to_use_bindactioncreators
---


https://medium.com/@kristenleach24/how-and-when-to-use-bindactioncreators-afe1f2d5f819

If you’ve ever used Redux with React, you likely already know that React components are completely unaware of Redux until you connect the two. For that, we use connect(); a function designed to do just that. However, it would be overkill to connect every individual component to the Redux store. It seems the best practice is to connect container components and pass that information down to their children as needed. This can be done by mapping the Redux state and actions to props in the parent container using mapStateToProps and mapDispatchToProps. MapStateToProps is pretty straightforward; you can use a spread operator and pass the entire Redux store as an object through as props to each child component, like this:


Similarly, once you have imported your actions file into the parent component, you can pass the actions as props using mapDispatchToProps. This function takes each action function you have written and wraps them in the Redux ‘dispatch’ function. Dispatch is the only function that will trigger a change in the Redux state. Thus, every action in your action file must be wrapped in the dispatch function, which will then fire the action, alert the reducer of the action type, and trigger those updates. If you want to dive deeper into how dispatch is working, you can read the Redux docs here. MapDispatchToProps looks similar to mapStateToProps, but again, requires that extra step of wrapping your functions in dispatch.


At the top of this file, I have imported my actions file as ‘searchActions.’ MapDispatchToProps is building an object with key values sharing the name of each function in my actions file. Those keys point to the action function wrapped in dispatch so that when passed to props the child components can access and call those actions without being explicitly connected to the Redux store! This is great, and super handy when you start building out more complex React/Redux apps. However; what happens when your action file starts getting REALLY big? Every time you add a function to your actions file, you have to return to each container that may use that function, and add another key: value pair to your mapDispatchToProps function that will wrap that new action in dispatch. That can be very tedious and time-consuming on these bigger apps, and it can easily lead to errors if you forget to add it in one parent component or another. Enter: bindActionCreators.


BindActionCreators is a really handy method when you are dealing with a lot of actions in an app. The above snippet is doing EXACTLY what we did in the original mapDispatchToProps snippet, however: with bindActionCreators, you can pass the entire action file as an object, and each function within that object will then be wrapped in a dispatch function for you! Therefore, if you find yourself continuously adding new action functions, you can skip the legwork of needing to return to the parent components and add your new functions to mapDispatchToProps each time. Pretty cool trick, huh? Here’s how to do it:


At the top of your file, be sure to import all of your actions using an *, and use ‘as’ to specify a name for your actions object. Import bindActionCreators from ‘redux’, and connect from ‘react-redux’ (these should already be a part of your npm package, but if they aren’t, be sure to install these node modules first!)


Next, you can mapStateToProps as usual. When setting mapDispatchToProps, you want to return a new object using the spread operator on bindActionCreators, and pass your actions object (that you named on import) along with dispatch. BindActionCreators will do the magic of wrapping each function with dispatch for you!

Now, we need to pass mapStateToProps and mapDispatchToProps to our connect function. Here is one more tip for you (this can be done with or without bindActionCreators). While it is perfectly acceptable to simply pass these new objects to the connect function like this:


When dealing with larger apps, you may want to organize all of these props a little more. You can name each TYPE of prop under key names so you can keep track of where each prop is coming from. For example:


This may seem a little confusing at face value, so let’s break it down. First, we are exporting default and calling the connect function with mapStateToProps and mapDispatchToProps as usual. However, then we see another set of parentheses containing three prop objects called stateProps, dispatchProps, and ownProps. StateProps and dispatchProps are objects created by the mapStateToProps and mapDispatchToProps functions respectively, and ownProps refers to, you guessed it; your OWN props that you may be passing through to the child components. By inserting an arrow function here, we can set these objects to a key name to make it easier to call them later. In the example above, we are passing the state props with a spread operator. We want to include them all, but dont need to set the object to a separate name (although you can if you want). We set the object ownProps to the key name ‘router,’ because router props come from react-router, and these are passed from parent to child like any other prop. Here I am just naming them router since they are the only props outside of state and dispatch in my app that are being passed down. Lastly, we are setting the dispatch props to the key name ‘actions.’ By setting these names, we can then call the props inside the children like so:


To keep it a bit more organized, instead of saying ‘this.props.fetchStartingLocation’, we can specify that this prop is located within the actions object so that we know it isn’t just another function being passed as a prop from the parent component. It’s just a bit of syntactic sugar to help you and those reading your code understand where to find each function should they need to access it.

I was really excited to learn about bindActionCreators; it saves time and prevents needless errors by preventing the need to go back and add functions to your mapDispatchToProps function with each new addition to your actions. Hopefully this helps you clean up your own React/Redux projects in the future!
