# Live Project

## Introduction
For the last two weeks of my time at the Tech Academy, I worked among other students in a team where, using the ASP.NET MVC and a code first Entity framework, 
we developed an interactive website for managing the content and productions for a theater acting company. The Project is divided into several comparmentalized areas,
the main three being: The production area, the rental area, and the blog area. The team members were divided into gropus and each group was then assignined 
to work on feautures involving one of these three main areas. Since a lot of the team members, including myself, joined the project in the middle of its life cycle,
there were plenty of back end and front end features yet to be implemented. I got to work on several front end stories and back end stories where I got the chance to 
learn a lot of useful skills when working with the ASP.NET framework, the Entity framework with a code first focus, the Bootstrap framework, and how to use Razor Syntax to build dynamic websites using the C# language.

Below, I will describe the stories I worked on along with code snippets, pictures and navigation links.

## Stories
* [Front End Stories](#front-end-stories)
* [Back End Stories](#back-end-stories)

## Front End Stories
* [Number of Developers](#number-of-developers)
* [Index Page Table](#index-page-table)
* [Create/Edit Page Form](#create/edit-page)
* [Accordion Effect](#accordion-effect)

### Number of Developers
I was tasked to create a JavaScript function that counted the number of names displayed on the SignIn page and display that number next to page header. I decided to create a function with two variables: one that was set equal to the span tag that would hold the number wanting to be dispplayed, and the other equal to the the length of div tag that held the total of p elements being counted. I then called the function on when the window loads to set the first variable being created and set it equal to the second variable, thus displaying the total number of p tags withing the div tag and display that number next to the page header. 

       <div class="py-5 text-center">
           @*Centered text and padded bottom*@

           <h1>Developers Of TheatreCMS &nbsp;<span id="NumPersons" class="badge badge-secondary">Total</span></h1>

           <h2>SignIn</h2>
              </div>
              @* Add your name to the bottom of the list like so: *@
                     @* <p>YOUR NAME</p> *@
                     <div class="Home-signin--namecontainer col-lg-12" id="PersonList">
                         <p>Raquel Rulli</p>
                         <p>Drew Slone</p>
                         <p>Emily-Maud Morris</p>
                         <p>Kevin McCrea</p>
                         <p>Jeffrey Arnold</p>
                         <p>Rhodri Thomas</p>
                         <p>Kevin Deming</p>
                         <p>Jaimie Bertoli</p>
                         <p>Dave Defourneaux</p>
                         <p>Cory Grundy</p>
                         <p>Brian Brown</p>
                         <p>Stephen Webb</p>
                         <p>Austin Riggs</p>
                         <p>Michael Shigezumi</p>
                         <p>Derek Threeton</p>
                         <p>Harrison Wayman</p>
                         <p>Garret Breitenbach</p>
                         <p>Daisy Salem</p>
                         <p>Garrett Henricks</p>
                         <p>Damon Flick</p>
                         <p>Matt Edey</p>
                         <p>Robert McCabe</p>
                         <p>Libby Bacon</p>
                         <p>Kristin Skelton</p>
                         <p>Desiree Fredenburg</p>
                         <p>Lyman McBride</p>
                         <p>Chris Robinson</p>
                         <p>Tyler Branscome</p>
                         <p>Kameron Jackson</p>
                         <p>Priyanka Thakan</p>
                         <p>Breanna Starika</p>
                         <p>Jacob Long</p>
                         <p>Maxim Ignatyev</p>
                         <p>Brian Reeves</p>
                         <p>Esie Vaughn</p>
                         <p>Adam Kelley</p>
                         <p>Jason Fors</p>
                         <p>Britnee Murrin</p>
                         <p>Alexander Sanderson</p>
                         <p>Michael Ford</p>
                         <p>Gary Matycich</p>
                         <p>Nathan Skiles</p>
                         <p>Cassie Peets</p>
                         <p>Cindy Lara</p>
                         <p>Joseph Omalley</p>
                         <p>Samuel Lehner</p>
                         <p>Keen Little</p>
                         <p>Philip Rivera</p>
                         <p>Ikaika Lock</p>
                         <p>Ash Kimsey</p>
                         <p>Jerry Nolazco</p>
                         <p>Daniel Warren</p>
                         <p>Wesley Paul</p>
                         <p>Steven Fralix</p>
                         <p>Thomas Curley</p>
                         <p>Paul Jamsa</p>
                         <p>Dominique Taylor</p>
                         <p>Joshua Ramos</p>
                         <p>Brittany Barnett</p>
                         <p>Jordan Medeiros</p>
                         <p>Ariel Rodriguez</p>
                         <p>Jeremy Munshower</p>
                         <p>Nick Pranno</p>
                         <p>Deepak Bandhu</p>
                         <p>Zachary Shick</p>
                         <p>Tabitha Yoerger</p>
                         <p>Ricardo Lopez</p>
                         <p>Eric Lemiere</p>
                         <p>Steven Novak</p>
                         <p>Joel Johnson</p>
                         <p>Kyle Knowles</p>
                         <p>Jason Storer</p>
                         <p>Kris Lovett</p>
                         <p>David Meyer</p>
                         <p>Carlos Briceno</p>
                         <p>Jaymes Pryor</p>
                         <p>Benjamin Stegall</p>
                         <p>Sophia Jordan</p>
                         <p>Kelsey Anderson</p>
                         <p>Sean Hager</p>
                         <p>Kyle Haugen</p>
                         <p>Ivan Fisher</p>
                         <p>Hailee Vandiver</p>
                         <p>Vinh Pham</p>
                         <p>Phil Marino</p>
                         <p>Jeff Stoppel</p>
                         <p>Raleigh C Johnson</p>
                         <p>Paul Fairbanks</p>
                         <p>Amy Ling</p>
                         <p>Gabriel Larson</p>
                         <p>Jacob Drawhorn</p>
                         <p>Hebron Shanko</p>
                         <p>Ivan Galas</p>
                         <p>Ryan Spears</p>
                         <p>Michael Tabb</p>
                         <p>Nicholas Perkins</p>
                         <p>Peter Galas</p>
                         <p>Peter Smith</p>
                         <p>Mamadou Kaly Bah</p>
                         <p>Jesse Kuykendall</p>
                         <p>Eric Boland</p>
                         <p>Iman Franklin</p>
                         <p>Dan Seymour</p>
                         <p>Tama Moors</p>
                         <p>Zachary Aars</p>
                         <p>Shalondra Rossiter</p>
                         <p>Cody Harris</p>
                         <p>Douglas Foreman</p>
                         <p>David Dixon</p>
                         <p>Eric Rymer</p>
                         <p>Jordan Arnold</p>
                         <p>Sanjeeta Thapa</p>
                         <p>Joseph Mckenna</p>
                         <p>Matthew White</p>
                         <p>Terry Nye</p>
                         <p>Kyle Crews</p>
                         <p>Corey Reid</p>
                         <p>Mallory Humphries</p>
                         <p>Tony Bongiovanni</p>
                         <p>Cody Keesee</p>
                         <p>Tien Nguyen</p>
                         <p>Joshua Watson</p>
                         <p>Daniel Alvarez</p>
                         <p>Carter Thurman</p>
                         <p>Spencer Merrill</p>
                         <p>Vicky Jones-Farias</p>
                         <p>Alain Lipowicz</p>
                         <p>Stephanie Drake</p>
                         <p>Duncan Robbins</p>
                         <p>Steve Irwin</p>
                         <p>Matt Clark</p>
                         <p>Cliff Carpenter</p>
                         <p>Carson Cook</p>
                         <p>Jonathan Gano</p>
                         <p>Jeremy DeLain</p>
                         <p>Robert Rodriguez</p>
                         <p>Aaron Twitty</p>
                         <p>Yogesh Gandhi</p>
                         <p>Jeff Alvarez</p>
                         <p>Travis Lord</p>
                         <p>Brady Pochon</p>
                         <p>Immanuel Hise</p>
                         <p>Erick Crowne</p>
                         <p>Mark Kaminskiy</p>
                         <p>Kim Tendulkar</p>
                         <p>Ny Arce</p>
                         <p>Josh Bowersock</p>
                         <p>Roman Paladiy</p>
                         <p>Hunter Grayson</p>
                         <p>Heather Shultz</p>
                         <p>Matt Farschman</p>
                         <p>Shalena Harris</p>
                         <p>Nathan Fidler</p>
                         <p>Alan Mitchell</p>
                         <p>Tanuj Chowdhury</p>
                         <p>Tim Seneker</p>
                         <p>Julianne Murdock</p>
                         <p>Lawrence McCary</p>
                         <p>Lizzy Esqueda</p>
                         <p>Alexander Pinon</p>
                         <p>Shaelynn Caltagirone</p>
                         <p>Tyler Hatch</p>
                         <p>Brynn Peirce</p>
                         <p>Carter Bacon</p>
                         <p>Matthew Singleton</p>
                         <p>Maher Dakdouk</p>
                         <p>Wade Johnson</p>
                         <p>Christdjin Brady</p>
                         <p>Quinn Davis</p>
                         <p>Nilesh Mepani</p>
                         <p>Jeffrey Licano</p>
                         <p>Grant Webb</p>
                         <p>Andrew Weber</p>
                         <p>Mirwais Sarwary</p>
                         <p>Brady Seme</p>
                         <p>Evelina Garcia</p>
                         <p>Hanh Le</p>
                         <p>James Bennett</p>
                         <p>Samantha Nixon</p>
                         <p>Daniel Castillo</p>
                         <p>Aaron Masse</p>
                         <p>John Michael Ternes</p>
                         <p>Keith Moore</p>
                         <p>Ramon Villafan</p>
                         <p>Jason Rodgers</p>
                         <p>Bradley Robles</p>
                         <p>Sarah Linsdall</p>
                         <p>Alejandra Lopez</p>
                         <p>Andy Panagos</p>
                         <p>Nate Dorgan</p>
                         <p>Jalen Allison</p>
                         <p>Spencer Davis</p>
                         <p>Stephen Brinkman</p>
                         <p>Aleksandr Yanyuk</p>
                         <p>Nikita Sazonov</p>
                         <p>Katherine Pak</p>
                         <p>Kai Wilder</p>
                         <p>Mohammad Nejad</p>
                         <p>Zelena Palijo</p>
                         <p>Madison Sailors</p>
                         <p>Luke Poag</p>
                         <p>Samantha Sargent</p>
                         <p>Vivienne Padilla</p>
                         <p>Ross Iverson</p>
                         <p>Brandon Roman</p>
                         <p>Leonardo Salazar</p>
                         <p>Jon Duea</p>
                         <p>Tina Morlock</p>
                         <p>Chase Martin</p>
                     </div>
                     
      function totalUsers() {
    var nameList = document.getElementById("PersonList");
    var numberOfNames = nameList.children.length;
    document.getElementById("NumPersons").innerHTML = numberOfNames;
    }
    window.onload = totalUsers();                     
       
### Index Page Table
I was tasked consisted on figuring out various elements of the object being tracked and create a model, a model form, and develop CRUD functionality to manage 
the data being entered by the user. I decided to create a Web apllication where the user could add locations in Costa Rica that they consider worth visiting. I created a model with different categories for the user to fill out when a location is addded.

       code snippet here...
       
### Create/Edit Page

       code snippet here...
       
### Accordiion Effect

       code snippet here...
              
*Jump to: [CRUD Functionality](#crud-functionality), [API](#api), [Front End Development](#front-end-development), [Page Top](#live-project)
*Jump to: [CRUD Functionality](#crud-functionality), [API](#api), [Front End Development](#front-end-development), [Page Top](#live-project)

## Back End Stories
* [CRUD Functionality](#crud-functionality)
* [Sorting Feature](#sorting-feature)
* [Restriction Feature](#restriction-feature)

### CRUD Functionality

       code snippet here...
       
### Sorting Feature

       code snippet here...
       
### Restriction Feature

       code snippet here...
              
*Jump to: [CRUD Functionality](#crud-functionality), [API](#api), [Front End Development](#front-end-development), [Page Top](#live-project)
*Jump to: [CRUD Functionality](#crud-functionality), [API](#api), [Front End Development](#front-end-development), [Page Top](#live-project)

## Another Important Skill
