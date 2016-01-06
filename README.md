# Concepts

## Overview

There are some core concepts that every Angular developer will need to familiarise themselves with. This will teach you the core concepts that you will be using in every Angular application you make.

## Objectives

- Define MVC, MVVM
- Describe two-way data-binding
- Demonstrate updating Models and Views without two-way binding
- Describe Angular's two-way binding with flow charts
- Describe Dependency Injection
- Describe Angular's Dependency Injection
- Describe a Single Page Application and common features
- Demonstrate server-side rendering concepts
- Describe Single Page Applications with Angular

## MVC/MVVM

You might have seen the term MVC/MVVM being thrown around. These stand for Model-View-Controller/Model-View-ViewModel respectively. These is how you architecture your software. They are both quite similar, however there are a few differences -

### MVC (Model-View-Controller)

Three parts to MVC; model, view, controller. The model manages the fundamental behaviours and data of the application. This could be retrieved from a database or any other sort of data store.

The view is the user interface. This takes data from the model and displays it nicely for the user. Any user interaction in the view is then handed over to the controller.

The controller receives user input and makes calls to the model and view to update/modify either. This keeps the main aspects of our application separate.

### MVVM (Model-View-ViewModel)

Similar to MVC, however the controller is replaced with a ViewModel.

The ViewModel is responsible for all view logic - changing the model data appropriately for use in the view. (For example, our model might contain a unix timestamp for a date but we need it in human readable format). Your model will contain all of your business logic, and your view is there to display your model (modified by the ViewModel).

MVVM is the preferred architecture when developing Angular applications, and it is what we will be using.

## Data-binding

Data-binding is the term for automatic synchronisation of data between the model and the view. This comes in two formats - one-way and two-way data-binding.

### One-way data-binding

Imagine you have a form input, asking for the user's name. You've also got a `<h2>` tag below, that you want to populate to say "Hey, {name}!". Wouldn't it be neat if this `<h2>` tag could update as the user types in their name? This is called one-way data-binding. The model (our user's name) is updated and our view is updated to reflect the change to our model.

Why isn't this two-way? Well, the `<h2>` tag populated with the user's name (model) will never update the model itself. Therefore, the flow of data goes from the input to the `<h2>` tag, but not from the `<h2>` tag to the input.

[Here's an example of one-way data-binding.](https://jsfiddle.net/6z6d5b7x/) 

### Two-way data-binding 

However, you have two-way data-binding when you bind your model value to an element that can both change and display the value of the model (such as an input).

You aren't restricted to updating your model value just in the `<input />` however - you can update this model value elsewhere (such as a "reset" button to reset the model) and it will be automatically reflected in the input (it will go blank).

[Checkout this example of two-way data-binding](https://jsfiddle.net/6z6d5b7x/1/)

You can see the flow of this here -

![Two-way data-binding](https://docs.angularjs.org/img/Two_Way_Data_Binding.png)

## Dependency Injection

Angular offers dependency injection. This allows us to request whatever Controller/Directive/etc. we want, instead of receiving them all in a specific order. This is not a default JavaScript behaviour. 

This is extremely powerful - it means that we can inject our custom Controllers etc. into all of our code, and have every dependency available in the application.

## Single Page Applications

Angular allows us to create single page applications (SPAs). The means that the user goes to one page and very rarely will have to refresh/leave that page to go to other parts of the website.

Single page applications handle all the routing, calling different parts of your codebase dependant on what URL the user is currently at.

Tranditionally, server-side rendering would be like the following -

![Server-side rendering](http://www.michaelgallego.fr/images/posts/2012-11-26-client-side-1.png)

With Angular, the flow will go like this instead -

![Client-side rendering](http://branchandbound.net/pics/client-side-rendering-only.png)

(this looks a lot more complicated, but it isn't!)

## Resources

- [AngularJS Dependency Injection Manual](https://docs.angularjs.org/guide/di)
- [AngularJS Databinding Documentation](https://docs.angularjs.org/guide/databinding)
