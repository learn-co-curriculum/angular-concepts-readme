# MVVM and Data Binding in Angular

## Overview

In this lesson, we are going to look at the core concepts that we will use in every Angular application. Some will be familiar to you, however some may seem a bit strange. Don't worry if they take time to sink in!

## Objectives

- Define MVC (Model-View-Controller), MVVM (Model-View-ViewModel) as they relate to both Single Page Applications and software programming in general
- Describe one-way and two-way data-binding that Angular utilizes and offers
- Describe Dependency Injection, a clever way to enable us to have what we want, wherever we want it
- Describe a Single Page Application and common features
- Demonstrate server-side rendering concepts

## Single Page Applications

Angular allows us to create single page applications (SPAs). The means that the user goes to one page and very rarely will have to refresh/leave that page to go to other parts of the website. Ever wondered how we can go to Twitter and never have to actually refresh the page? Yet all of our notifications, tweets, etc are all real-time and constantly up-to-date? You guessed it - Twitter is a single page application!

Single page applications handle all the routing, calling different parts of your codebase depending on what URL the user is currently at. If we look back at Twitter, you'll notice how the URL does change yet the page doesn't refresh. This is because we have now handed all routing over to the client side instead of the server. The client can see where the user has intended to go, and select the specific code for that page - magical!

Tranditionally, server-side rendering would be like the following -

![Server-side rendering](http://www.michaelgallego.fr/images/posts/2012-11-26-client-side-1.png)

The user requests the page from the server, and the server will return all the HTML to display on that page. The data would not be updated until the user refreshes. This puts overhead on the server, as it will have to render the page on every page load. If you head over to the [BBC News](http://bbc.co.uk/news) you'll see how the content is already there - no waiting whatsoever.

With Angular, the flow will go like this instead -

![Client-side rendering](http://branchandbound.net/pics/client-side-rendering-only.png)

This looks a lot more complicated, but it isn't! Instead of returning rendered HTML for each user, the server would return the same page for every user. The client will then make a request to the server, requesting what's necessary for that page to render (such as a list of products). The client will then render this page for the user.

This has massive advantages - if 1000 users are on the website, instead of one server rendering 1000 pages, 1000 clients are rendering one page, reducing strain on the server. We can also re-use backend endpoints - our mobile website and our desktop website can both request the same data from the server but display it differently.

One example of this that you can check out for yourself is if you go to Facebook. You might notice how you don't actually see anything until the content very quickly loads and then the client renders this - saving so many resources in the meantime!

## MVC/MVVM

You might have seen the terms MVC and MVVM being thrown around. These stand for Model-View-Controller and Model-View-ViewModel respectively. 

These are concepts for how we architect our software. We do this to promote separation of concerns. Separation of concerns is dividing our code into logical chunks, with each chunk addressing a separate concern. This allows us to create testable, reusable and scalable well designed code.

They are both quite similar, however there are a few differences -

### MVC (Model-View-Controller)

Three parts to MVC; model, view, controller. The model manages the fundamental behaviours and data of the application. This could be retrieved from a database or any other sort of data store.

The view is the user interface. This takes data from the model and displays it nicely for the user. Any user interaction in the view is then handed over to the controller.

The controller receives user input and makes calls to the model and view to update/modify either. This keeps the main aspects of our application separate.

An easy way to visualize this is if we imagine we are ordering a coffee. The Model is the information about the drink we've ordered, the Controller is the barista and the View is the finished drink. The barista would make the drink from our order (the Model), and serve it to us (the View).

So for example, if you walked into a coffee bar and ordered a hot chocolate, you'd get a hot chocolate. If you then wanted marshmallows, you'd ask the barista, who would go back to the till and modify your order to add on marshmallows. They would also then put marshmallows in your drink, and return you the updated drink (the View).

If we weren't using a single page application and instead the server was rendering the page for us, the barista would have simply thrown out the drink and remade it with marshmallows - what a waste!  

If you've touched on MVC before, you might have learnt it a little differently. Not to worry! MVC in the frontend is slightly different, but the main concepts still apply!

### MVVM (Model-View-ViewModel)

Similar to MVC, however the controller is replaced with a ViewModel.

Let's take a trip back to the coffee shop. You'll notice there is a new member of staff - a cashier. The barista was too overloaded as a controller, and has stepped down to just being a helper. The cashier has been brought in as a ViewModel, in order to make the coffee shop more efficient.

Like before, we order a hot chocolate. The cashier takes your order, updating the Model. They then shout to the barista that they need a hot chocolate. The barista makes the hot chocolate, and returns it to the cashier. The cashier then writes your name on the lid, and returns it to you.

The differences here is that we no longer have one person taking your order and delivering your drink. Instead, the cashier (ViewModel) uses a helper (business logic) to get your drink order (Model) completed and only modifies the lid with your name (view logic) and returns it to you (the View).

This is the preferred architecture for Angular applications. Why? We no longer have a controller doing everything for us. Instead, we can simplify the application down massively by having helpers that we can use everywhere.

The ViewModel is responsible for all view logic - changing the model data appropriately for use in the view. (For example, our model might contain a UNIX timestamp for a date but we need it in human readable format). Your model will contain all of your business logic, and your view is there to display your model (modified by the ViewModel).

## Data-binding

Data-binding is the concept that allows us to easily keep our view and model synchronised without having to write excessive amounts of code whenever we would like to update either. This comes in two formats - one-way and two-way data-binding.

### One-way data-binding

Imagine you have a form input, asking for the user's name. You've also got a `<h2>` tag below, that you want to populate to say "Hey, {name}!". Wouldn't it be neat if this `<h2>` tag could update as the user types in their name? This is called one-way data-binding. The model (our user's name) is updated and our view is updated to reflect the change to our model.

For example, you'd use one-way data-binding when you've got a search box - the user can type in their search query and the title can change to "Results for: {searchQuery}" - pretty cool!

[Here's an example of one-way data-binding.](https://jsfiddle.net/6z6d5b7x/)
 
An easy way to visualize this is to go back to when we were receiving our drink from the barista. If the drink was one-way bound from the barista, the drink would always be updated and correct. However, the barista wouldn't be able to see the drink. If it got knocked over or was mouldy, the barista wouldn't have any idea!

### Two-way data-binding 

Two-way data-binding occurs when you bind your model value to an element that can both change and display the value of the model (such as an input).

You aren't restricted to updating your model value just in the `<input />` however - you can update this Model value elsewhere (such as a "reset" button to reset the model) and it will be automatically reflected in the input (it will go blank).

[Checkout this example of two-way data-binding](https://jsfiddle.net/6z6d5b7x/1/)

You can see the flow of this here -

![Two-way data-binding](https://docs.angularjs.org/img/Two_Way_Data_Binding.png)

Going back to our barista - with two-way data-binding, our barista can now see everything! If our drink was to get knocked over after given to us, the barista would notice and be able to act upon that wild change of events!

Two-way data-binding has a one-directional flow of data which ensures that the View and the Model data is always synchronized.

In the above example our template compiles to become our View, which is a representation of the Model data. The View can then change our Model (for instance, an `<input />` being updated), which then updates our View. Model changes drive View changes and View changes drive Model changes. This keeps everything always synchronized. 

## Resources

- [AngularJS Dependency Injection Manual](https://docs.angularjs.org/guide/di)
- [AngularJS Databinding Documentation](https://docs.angularjs.org/guide/databinding)

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/angular-concepts-readme'>Angular Concepts</a> on Learn.co and start learning to code for free.</p>
