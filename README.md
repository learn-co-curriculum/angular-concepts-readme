# Angular Core Concepts

## Overview

In this lesson, we are going to look at the core concepts that we will use in every Angular application. Some will be familiar to you, however some may seem a bit strange. Don't worry if they take time to sink in!

## Objectives

- Define MVC (Model-View-Controller), MVVM (Model-View-ViewModel)
- Describe one-way and two-way data-binding
- Describe Angular's two-way binding
- Describe Dependency Injection
- Describe a Single Page Application and common features
- Demonstrate server-side rendering concepts

## Single Page Applications

Angular allows us to create single page applications (SPAs). The means that the user goes to one page and very rarely will have to refresh/leave that page to go to other parts of the website.

Single page applications handle all the routing, calling different parts of your codebase dependant on what URL the user is currently at.

Tranditionally, server-side rendering would be like the following -

![Server-side rendering](http://www.michaelgallego.fr/images/posts/2012-11-26-client-side-1.png)

The user requests the page from the server, and the server will return all the HTML to display on that page. The data would not be updated until the user refreshes. This puts overhead on the server, as it will have to render the page on every page load.

With Angular, the flow will go like this instead -

![Client-side rendering](http://branchandbound.net/pics/client-side-rendering-only.png)

This looks a lot more complicated, but it isn't! Instead of returning rendered HTML for each user, the server would return the same page for every user. The client will then make a request to the server, requesting what's necessary for that page to render (such as a list of products). The client will then render this page for the user.

This has massive advantages - if 1000 users are on the website, instead of one server rendering 1000 pages, 1000 clients are rendering one page, reducing strain on the server. We can also re-use backend endpoints - our mobile website and our desktop website can both request the same data from the server but display it differently.

## MVC/MVVM

You might have seen the term MVC/MVVM being thrown around. These stand for Model-View-Controller/Model-View-ViewModel respectively. 

These are concepts for how we architecture our software. We do this to promote separation of concerns. Separation of concerns is dividing our code into logical chunks, with each chunk addressing a separate concern. This allows us to create testable, reusable and scalable well designed code.

They are both quite similar, however there are a few differences -

### MVC (Model-View-Controller)

Three parts to MVC; model, view, controller. The model manages the fundamental behaviours and data of the application. This could be retrieved from a database or any other sort of data store.

The view is the user interface. This takes data from the model and displays it nicely for the user. Any user interaction in the view is then handed over to the controller.

The controller receives user input and makes calls to the model and view to update/modify either. This keeps the main aspects of our application separate.

As easy way to visualize this is if we imagine we are ordering a coffee. The Model is the information about the drink we've ordered, the Controller is the barista and the View is the finished drink. The barista would make the drink from our order (the Model), and serve it to us (the View).

So for example, if you walked into a coffee bar and ordered a hot chocolate, you'd get a hot chocolate. If you then wanted marshmallows, you'd ask the barista, who would go back to the till and modify your order to add on marshmallows. They would also then put marshmallows in your drink, and return you the updated drink (the View).

### MVVM (Model-View-ViewModel)

Similar to MVC, however the controller is replaced with a ViewModel.

The ViewModel is responsible for all view logic - changing the model data appropriately for use in the view. (For example, our model might contain a unix timestamp for a date but we need it in human readable format). Your model will contain all of your business logic, and your view is there to display your model (modified by the ViewModel).

Let's take a trip back to the coffee shop. You'll notice there is a new member of staff - a cashier. The barista was too overloaded as a controller, and has stepped down to just being a helper. The cashier has been brought in as a ViewModel, in order to make the coffee shop more efficient.

Like before, we order a hot chocolate. The cashier takes your order, updating the Model. They then shout to the barista that they need a hot chocolate. The barista makes the hot chocolate, and returns it to the cashier. The cashier then writes your name on the lid, and returns it to you.

The differences here is that we no longer have one person taking your order and delivering your drink. Instead, the cashier (ViewModel) uses a helper (business logic) to get your drink order (Model) completed and only modifies the lid with your name (view logic) and returns it to you (the View).

This is the preferred architecture for Angular applications. Why? We no longer have a controller doing everything for us. Instead, we can simplify the application down massively by having helpers that we can use everywhere.

## Data-binding

Data-binding is the term for automatic synchronisation of data between the model and the view. This comes in two formats - one-way and two-way data-binding.

### One-way data-binding

Imagine you have a form input, asking for the user's name. You've also got a `<h2>` tag below, that you want to populate to say "Hey, {name}!". Wouldn't it be neat if this `<h2>` tag could update as the user types in their name? This is called one-way data-binding. The model (our user's name) is updated and our view is updated to reflect the change to our model.

For example, you'd use one-way data-binding when you've got a search box - the user can type in their search query and the title can change to "Results for: {searchQuery}" - pretty cool!

[Here's an example of one-way data-binding.](https://jsfiddle.net/6z6d5b7x/) 

### Two-way data-binding 

Two-way data-binding occurs when you bind your model value to an element that can both change and display the value of the model (such as an input).

You aren't restricted to updating your model value just in the `<input />` however - you can update this Model value elsewhere (such as a "reset" button to reset the model) and it will be automatically reflected in the input (it will go blank).

[Checkout this example of two-way data-binding](https://jsfiddle.net/6z6d5b7x/1/)

You can see the flow of this here -

![Two-way data-binding](https://docs.angularjs.org/img/Two_Way_Data_Binding.png)

Two-way data-binding has a one-directional flow of data which ensures that the View and the Model data is always synchronized.

In the above example our template compiles to become our View, which is a representation of the Model data. The View can then change our Model (for instance, an `<input />` being updated), which then updates our View. Model changes drive View changes and View changes drive Model changes. This keeps everything always synchronized. 

## Dependency Injection

Angular offers dependency injection. This allows us to request whatever Controller/Directive/etc. we want, instead of receiving them all in a specific order. This is not a default JavaScript behaviour. 

This is extremely powerful - it means that we can inject our custom Controllers etc. into all of our code, and have every dependency available in the application.

We will revisit Dependency Injection later on, in greater detail.

## Resources

- [AngularJS Dependency Injection Manual](https://docs.angularjs.org/guide/di)
- [AngularJS Databinding Documentation](https://docs.angularjs.org/guide/databinding)
