# Live Project

## Introduction
For the last two weeks of my time at the Tech Academy, I worked among other students in a team where, using the ASP.NET MVC and a code first Entity framework, 
we developed an interactive website for managing the content and productions for a theater acting company. The Project is divided into several comparmentalized areas,
the main three being: The production area, the rental area, and the blog area. The team members were divided into gropus and each group was then assignined 
to work on feautures involving one of these three main areas. Since a lot of the team members, including myself, joined the project in the middle of its life cycle,
there were plenty of back end and front end features yet to be implemented. I got to work on several front end stories and back end stories where I got the chance to 
learn a lot of useful skills when working with the ASP.NET framework, the Entity framework with a code first focus, the Bootstrap framework, and how to use Razor Syntax
to build dynamic websites using the C# language.

Below, I will describe the stories I worked on along with code snippets, pictures and navigation links.

## Stories
* [Front End Stories](#front-end-stories)
* [Back End Stories](#back-end-stories)


* [CRUD Functionality](#crud-functionality)
* [API](#api)
* [Front End Development](#front-end-development)

## Front End Stories

### Story

       code snippet here...

*Jump to: [CRUD Functionality](#crud-functionality), [API](#api), [Front End Development](#front-end-development), [Page Top](#live-project)

## Back End Stories

### Story

       code snippet here...

*Jump to: [CRUD Functionality](#crud-functionality), [API](#api), [Front End Development](#front-end-development), [Page Top](#live-project)



### CRUD Functionality
This task consisted on figuring out various elements of the object being tracked and create a model, a model form, and develop CRUD functionality to manage 
the data being entered by the user. I decided to create a Web apllication where the user could add locations in Costa Rica that they consider worth visiting. I created a model with different categories for the user to fill out when a location is addded.

       code snippet here


I then created a base html page and, by using template inheridtance along with template tags, I created a home page among other pages that allows the user to add, edit, and delete locations within the app. Then, using URL routing, each of the pages urls were mapped to a view based function to display the desired content when the user requests a page within the app. Below is an example the page to add a location followed by the function used that renders the page when requested by the user:
  
  
        code snippet here

*Jump to: [CRUD Functionality](#crud-functionality), [API](#api), [Front End Development](#front-end-development), [Page Top](#live-project)

### API
Another one of the tasks was to create a page within the app where information from an API was presented to the user using JSON responses and url/http 
queries that relates to the chosen topic in some way. As I added a "Cost" field within the form to add locations, I decided to use an API that realtes to currency rate exchanges to allow users to select from a list menu of a currency and view the exchange rate the chosen currency to Colones (the currency used in Costa Rica. I created a page template and a fuction to render the API page when requested. Withing the template, I created a select menu that lists the top ten currencies used around the world as a way to get user input information. Then, by parsing through the JSON file returned by the API, I querried specific information from the API to display the desired exchange rate based on the user's selected currency (user's input). Below I have attached the function used when the API page is requested:

  
        code snippet here
            
 
*Jump to: [CRUD Functionality](#crud-functionality), [Front End Development](#front-end-development), [Page Top](#live-project)
