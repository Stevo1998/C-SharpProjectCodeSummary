# Live Project

## Introduction
For the last two weeks of my time at the Tech Academy, I worked among a team where, using the ASP.NET MVC and a code first Entity framework, 
we developed an interactive website for managing the content and productions for a theater acting company. The Project was divided into several comparmentalized areas,
the main three being: The production area, the rental area, and the blog area. The team members were divided into gropus and each group was then assignined 
to work on feautures involving one of these three main areas. Since a lot of the team members, including myself, joined the project in the middle of its life cycle,
there were plenty of back end and front end features yet to be implemented. I got to work on several front end stories and back end stories where I got the chance to 
learn a lot of useful skills when working with the ASP.NET framework, the Entity framework with a code first focus, the Bootstrap framework, and how to use Razor Syntax to build dynamic websites using the C# language.

Below, I will describe the stories I worked on along with code snippets and navigation links.


## Stories
* [Back End Stories](#back-end-stories)
* [Front End Stories](#front-end-stories)

## Important Skills
* [Other Important Skills](#other-important-skills)


### Back End Stories
* [CRUD Functionality](#crud-functionality)
* [Sorting Feature](#sorting-feature)
* [Restriction Feature](#restriction-feature)

#### CRUD Functionality
In this story, I tasked with creating an entity model for the retal area of the page and then add scaffolding pages to provide CRUD functionality to the user.
First, I created a model fo the rental area thatt specified the names and types of variables that can exist in an object being created. This variables would then
be used to create, edit, delete, or view details of an object being created in the rental area of the page.

       namespace TheatreCMS3.Areas.Rent.Models
       {
           public class RentalHistory
           {
               public int RentalHistoryId { get; set; } /* Primary Key on Table */  
               public bool RentalDamaged { get; set; }
               public string DamageIncurred { get; set; }
               public string Rental { get; set; }
           }
       }
 
Second, I used the index page for the rental area to diplay a table where the user could create an object by providing the value for the variables defined in the
model. Once an object was created, the table would then display this object along with links to give the object CRUD capabilities.

      <h2>Index</h2>
       <p>
           @Html.ActionLink("Create New", "Create")
       </p>
       <table class="table">
           <tr>
               <th>
                   @Html.DisplayNameFor(model => model.RentalDamaged)
               </th>
               <th>
                   @Html.DisplayNameFor(model => model.DamageIncurred)
               </th>
               <th>
                   @Html.DisplayNameFor(model => model.Rental)
               </th>
               <th></th>
           </tr>
           @foreach (var item in Model) 
            {
               <tr>
                   <td>
                       @Html.DisplayFor(modelItem => item.RentalDamaged)
                   </td>
                   <td>
                       @Html.DisplayFor(modelItem => item.DamageIncurred)
                   </td>
                   <td>
                       @Html.DisplayFor(modelItem => item.Rental)
                   </td>
                   <td>
                       @Html.ActionLink("Edit", "Edit", new { id=item.RentalHistoryId }) |
                       @Html.ActionLink("Details", "Details", new { id=item.RentalHistoryId }) |
                       @Html.ActionLink("Delete", "Delete", new { id=item.RentalHistoryId })
                   </td>
               </tr>
            }
       </table>
       
#### Sorting Feature
In this story I was asked to add a sorting feature to the table being displayed on the index page of the rental area. The page had to display the histories created from newest to oldest and also have the capability to sort the table contents from A-Z, Z-A, damaged first, and undamaged first. I decided to accompplish this by changing the GET method for the index page within the controller for rhis area. I added a swtich statement to the method, and by using a different parameters from the query string in the URL the switch stament will choose one of the cases to return to the View, thus changing the order of the content in the table. 

       // GET: Rent/RentalHistories
        public ActionResult Index(string sortOrder)
        {
            ViewBag.IdSortParm = String.IsNullOrEmpty(sortOrder) ? "Id" : "";
            ViewBag.DamagedSortParm = sortOrder == "Damaged Rentals" ? "" : "Damaged Rentals";
            ViewBag.UndamagedSortParm = sortOrder == "Undamaged Rentals" ? "" : "Undamaged Rentals";
            ViewBag.AzSortParm = sortOrder == "Rentals A-Z" ? "" : "Rentals A-Z";
            ViewBag.ZaSortParm = sortOrder == "Rentals Z-A" ? "" : "Rentals Z-A"; 
            
            var rentals = from r in db.RentalHistories
                         select r;
            switch (sortOrder)
            {
                case "Id":
                    rentals = rentals.OrderByDescending(r => r.RentalHistoryId);
                    break;
                case "Damaged Rentals":
                    rentals = rentals.OrderBy(r => r.RentalDamaged == false);
                    break;
                case "Undamaged Rentals":
                    rentals = rentals.OrderBy(r => r.RentalDamaged == true);
                    break;
                case "Rentals A-Z":
                    rentals = rentals.OrderBy(r => r.Rental);
                    break;
                case "Rentals Z-A":
                    rentals = rentals.OrderByDescending(r => r.Rental);
                    break;
                default:
                    rentals = rentals.OrderByDescending(r => r.RentalHistoryId);
                    break;
            }
            return View(rentals.ToList());
        }
       
#### Restriction Feature
The main goal of this task was to prevent any user from accessing the create, edit, and delete pages unless permission was granted to them.

The first part of this task (the first story) was to create a new model for the rental area that enhiridted from the ApplicationUser class within the project in order
to create a manager role that acts as an admin to keep track of the histories of returned rentals. Then using this class a seed method was created where a manager role is created that seeds this user to the configuration file and records it in its databse. 
       
       public class HistoryManager : ApplicationUser
       {
              public int RestrictedUsers { get; set; }
              public int RentalReplacementRequests { get; set; }
              
              public static void Seed(ApplicationDbContext Mycontext)
              {
              var roleManager = new RoleManager<IdentityRole>(new RoleStore<IdentityRole>(Mycontext));
              var userManager = new UserManager<ApplicationUser>(new UserStore<ApplicationUser>(Mycontext));

              // Creating a HistoryManager role
              var role = new IdentityRole();
              role.Name = "HistoryManager";
              roleManager.Create(role);

              // Instantiating an object of History Manager / Creating an User
              var user = new HistoryManager
              {
                UserName = "Name",
                Email = "name@mail.com",
                RestrictedUsers = 2,
                RentalReplacementRequests = 1
              };
              var userPassword = "password";
              var manager = userManager.Create(user, userPassword);
              if(manager.Succeeded) { userManager.AddToRole(user.Id, "HistoryManager"); }
        }
    }
    
Then I created a class with a method that redirects the user to a created view displaying the restricted page when an unauthrized user tries to access any of the restricted pages.

       public class RentalHistoryAuthorization : AuthorizeAttribute
    {
        public string ViewName = "~/Rent/RentalHistories/AccessDenied";

        protected override void HandleUnauthorizedRequest(AuthorizationContext filterContext)
        {
            filterContext.Result = new RedirectResult(ViewName);
        }

        public override void OnAuthorization(AuthorizationContext filterContext)
        {
            if (AuthorizeCore(filterContext.HttpContext))
            {
                base.OnAuthorization(filterContext);
            }
            else
            {
                HandleUnauthorizedRequest(filterContext);
            }
        }

    }
    
The view that the user is redirected to:

      @model TheatreCMS3.Areas.Rent.Models.RentalHistory
       @{
           ViewBag.Title = "AccessDenied";
           Layout = "~/Views/Shared/_Layout.cshtml";
       }
       <div class="RentalHistory-AccessDenied--MainContainer">
           <div class="RentalHistory-AccessDenied--mainHeading">
               <h1>You are not authorized to visit that page.</h1>
           </div>
           <div class="img-fluid mx-auto">
               <img class="RentalHistory-AccessDenied--accessDeniedImage" src="~/Content/images/access_denied.png" alt="Access Denied" />
           </div>
           <div class="RentalHistory-AccessDenied--secondHeading">
               <button type="button" class="RentalHistory-AccessDenied--loginButton">
                   <h2>@Html.RouteLink("Login", new { action = "Login", controller = "Account", area = "" })</h2>
               </button>
           </div>
       </div>
              
*Jump to: [Back End Stories](#back-end-stories), [Front End Stories](#front-end-stories), [Page Top](#live-project)

### Front End Stories
* [Number of Developers](#number-of-developers)
* [Index Page Table](#index-page-table)
* [Create/Edit Page Form](#create/edit-page)
* [Accordion Effect](#accordion-effect)

#### Number of Developers
I was tasked to create a JavaScript function that counted the number of names displayed on the SignIn page and display that number next to page header. I decided to create a function with two variables: one that was set equal to the span tag that would hold the number wanting to be dispplayed, and the other equal to the the length of div tag that held the total of p elements being counted. I then called the function on when the window loads to set the first variable being created and set it equal to the second variable, thus displaying the total number of p tags withing the div tag and display that number next to the page header. 

<details>
       <summary>The HTML doc:</summary>
       
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
       
</details>

The JavaScript funtion:

      function totalUsers() {
    var nameList = document.getElementById("PersonList");
    var numberOfNames = nameList.children.length;
    document.getElementById("NumPersons").innerHTML = numberOfNames;
    }
    window.onload = totalUsers();                     
       
#### Index Page Table
This story required me to change the way the table in the index page was displayed to the user to better match the theme of the overall project page. There was numerous requirements the table should contain: I was asked for the table to display a red X or a green check depending on if the rental history being created was damaged or not, the name of the rental had to be styled to be displayed differently from the rest of the table elements, add a vertical elipsis icon to display the
action links that redireect to CRUD pages, and also use an elipssis efecr to prevent the damages description from wrapping on more than one line. I decided to edit
the table using a combiantion of CSS and bootstrap classes along with Razor Syntax whiting the document to meet all the requirements and Font-Awesome to display various icons within the page.

      <div class="RentalHistory-Index--TableContainer">
         <table class="RentalHistory-Index--Table">
           <tr>
             <th colspan="4">
               Most recent Rental Histories
             </th>
           </tr>

           @foreach (var item in Model)
            {
                 <tr>
                       <td>
                           @{var itemType = item.RentalDamaged;}
                           @if (itemType == true) @*If rental is damaged - red X*@
                            {
                               <i class="fa fa-times-circle">@Html.DisplayFor(modelItem => item.RentalDamaged)</i>
                            }
                            else @*If rental is not damaged - green check*@
                            {
                               <i class="fa fa-check-circle">@Html.DisplayFor(modelItem => item.RentalDamaged)</i>
                            }
                       </td>
                       <td>
                           <div class="badge badge-dark">@Html.DisplayFor(modelItem => item.Rental)</div>
                       </td>
                       <td>
                           <div class="ellipsis">@Html.DisplayFor(modelItem => item.DamageIncurred)</div> @*Ellipsis class to prevent more than one line*@
                       </td>
                       <td>
                           <div class="dropdown">
                               <button class="btn btn-dark" type="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                                   <i class="fas fa-ellipsis-v"></i> @*Ellipsis icon containing CRUD links*@                                
                               </button>
                               <div class="dropdown-menu dropdown-menu-right" aria-labelledby="dropdownMenuButton">
                                   <div class="dropdown-item">
                                       <i class="fa fa-pencil-square-o"></i>@Html.ActionLink("Edit", "Edit", new { id = item.RentalHistoryId })
                                   </div>
                                   <div class="dropdown-item">
                                       <i class="fa fa-info-circle"></i>@Html.ActionLink("Details", "Details", new { id = item.RentalHistoryId })
                                   </div>
                                   <br />
                                   <div class="dropdown-item">
                                       <div class="delete">
                                           <i class="fa fa-trash"></i>@Html.ActionLink("Delete", "Delete", new { id = item.RentalHistoryId })
                                       </div>
                                   </div>
                               </div>
                           </div>
                       </td>
                 </tr>
            }
         </table>
      
#### Create/Edit Page
In this story I was tasked to style the create and edit pages for the rental area to better match the overall theme of the project and make it more simple for 
the user to inoput the required variables for the model. I edited the form contained in this pages to meet all the requirements ggiven by the story. Some fields
within the form had be changed around, also the max width of the form had to be restricted to 600 pixels, all the buttons had to be placed inside the form, and the label that contained a check box to field to mark if a rental was damaged or not had to dynamically change upon user input. If the box was checked the label would display "Damaged?", else it would display notes. I used CSS to meet most of the requirements in this story. However, I used a JavaScript funtion, along with an onclick event to call it, to dynamically change the label above the checkbox field.

The HTML doc:

       @using (Html.BeginForm()) 
       {
           @Html.AntiForgeryToken()

           <div id="RentalHistory--Create--Form" class="form-horizontal">
               <hr />
               @Html.ValidationSummary(true, "", new { @class = "text-danger" })

               <div class="RentalHistory--Create--formGroupSplit">
                   <div class="RentalHistory--Create--column">
                       @Html.LabelFor(model => model.Rental, htmlAttributes: new { @class = "control-label col-md-2" })
                       <div class="RentalHistory--Create--colmd10">
                           @Html.EditorFor(model => model.Rental, new { htmlAttributes = new { @class = "form-control" } })
                           @Html.ValidationMessageFor(model => model.Rental, "", new { @class = "text-danger" })
                       </div>
                   </div>
                   <div class="RentalHistory--Create--column">
                       <label class="control-label col-md-2">Damaged?</label>
                       <div class="RentalHistory--Create--colmd10">
                           <div class="RentalHistory--Create--checkbox" onclick="notesToDamage('RentalDamaged','labelText')"> @*Calls JS Func on click*@
                               @Html.EditorFor(model => model.RentalDamaged)
                               @Html.ValidationMessageFor(model => model.RentalDamaged, "", new { @class = "text-danger" })
                           </div>
                       </div>
                   </div>
               </div>

               <div class="form-group">
                   <label id="labelText" class="RentalHistory--Create--colmd2 control-label mt-3">Notes</label>
                   <div class="RentalHistory--Create--colmd10">
                       @Html.EditorFor(model => model.DamageIncurred, new { htmlAttributes = new { @class = "form-control" } })
                       @Html.ValidationMessageFor(model => model.DamageIncurred, "", new { @class = "text-danger" })
                   </div>
               </div>

               <div class="RentalHistory--Create--dflex justify-content-center">
                   <button type="button" class="btn btn-dark">
                       @Html.ActionLink("Back to List", "Index")
                   </button>
                   <input type="submit" value="Create" class="btn btn-success" />
               </div>
           </div>
       }
       
The JavaScript function:

      // Function to change the label on the Create and Edit Form depending on checkbox
       function notesToDamage(thecheckbox, thelabel) {

           var checkbox = document.getElementById(thecheckbox);
           var label = document.getElementById(thelabel);
           if (!checkbox.checked) {
               label.innerHTML = "Notes";
           }
           else {
               label.innerHTML = "Damages Incurred";
           }
       }
      
#### Accordion Effect
This story consisted of adding an accordion effect to the table on the index page of the retal area. As the table displays a history of the rented items, next to the name of the rental I was tasked to display the damages incurred next to the name of each rented item, if no damages were incurred then display "None". Also, if no damages were incurred to an item, then an accordion effect was used to display the notes/details on that item inputed by the user/renter. To complete this story, I modified various table elements using the bootstrap framework to show the notes/details row on the table when the user clicks on an item and autohide when the user clicks on another.

      <div id="myAccordion" class="RentalHistory-Index--TableContainer">
          <table id="indexTable" class="RentalHistory-Index--Table">
              <tr>
                  <th colspan="4">
                      Most recent Rental Histories
                          <div class="float-right">
                              <label>Sorted By:</label>
                                  <button class="btnMargin btn btn-dark dropdown-toggle " type="button" id="dropdownMenuButton" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                                      No Extra Sorting...
                                  </button>
                                  <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
                                      <div class="dropdown-item">@Html.ActionLink("No Extra Sorting...", "Index", new { sortOrder = ViewBag.IdSortParm })</div>
                                      <div class="dropdown-item">@Html.ActionLink("Damaged Rentals", "Index", new { sortOrder = ViewBag.DamagedSortParm })</div>
                                      <div class="dropdown-item">@Html.ActionLink("Undamaged Rentals", "Index", new { sortOrder = ViewBag.UndamagedSortParm })</div>
                                      <div class="dropdown-item">@Html.ActionLink("Rentals A-Z", "Index", new { sortOrder = ViewBag.AzSortParm })</div>
                                      <div class="dropdown-item">@Html.ActionLink("Rentals Z-A", "Index", new { sortOrder = ViewBag.ZaSortParm })</div>
                                  </div>
                           </div>
                    </th>
             </tr>

             @foreach (var item in Model)
             {
                 <tr>
                     <td>
                         @{ var itemType = item.RentalDamaged; }
                         @if (itemType == true)
                         {
                             <i class="fa fa-times-circle">@Html.DisplayFor(modelItem => item.RentalDamaged)</i>
                         }
                         else
                         {
                             <i class="fa fa-check-circle">@Html.DisplayFor(modelItem => item.RentalDamaged)</i>
                         }
                     </td>
                     <td>
                         <div class="badge badge-dark">@Html.DisplayFor(modelItem => item.Rental)</div>
                     </td>
                     <td>
                         @{ var description = item.DamageIncurred; }
                         @{ var damage = item.RentalDamaged; }
                         @if (damage == false)
                         {
                             <div id="heading-@item.RentalHistoryId">
                                 <div data-toggle="collapse" data-target="#collapse-@item.RentalHistoryId" aria-expanded="false" aria-controls="collapse-@item.RentalHistoryId">None.</div>
                            </div>
                         }
                         else
                         {
                             <div class="text-truncate">@Html.DisplayFor(modelItem => item.DamageIncurred)</div>
                         }
                     </td>
                     <td>
                         <div class="dropdown">
                             <button class="btnMargin btn btn-dark" type="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false"><i class="fas fa-ellipsis-v"></i></button>
                             <div class="dropdown-menu dropdown-menu-right" aria-labelledby="dropdownMenuButton">
                                 <div class="dropdown-item">
                                     <i class="fa fa-pencil-square-o"></i>@Html.ActionLink("Edit", "Edit", new { id = item.RentalHistoryId })
                                 </div>
                                 <div class="dropdown-item">
                                     <i class="fa fa-info-circle"></i>@Html.ActionLink("Details", "Details", new { id = item.RentalHistoryId })
                                 </div>
                                 <br />
                                 <div class="dropdown-item">
                                     <div class="delete">
                                         <i class="fa fa-trash"></i>@Html.ActionLink("Delete", "Delete", new { id = item.RentalHistoryId })
                                     </div>
                                 </div>
                             </div>
                         </div>
                     </td>
                 </tr>
                 <tr id="collapse-@item.RentalHistoryId" class="collapse" aria-labelledby="heading-@item.RentalHistoryId" data-parent="#myAccordion">
                     <td class="RentalHistory-Index--HiddenCell" colspan="4">
                         <div class="RentalHistory-Index--textTruncate">
                             @Html.DisplayFor(modelItem => item.DamageIncurred)
                         </div>  
                     </td>
                 </tr>
              }        
         </table>
     </div>
              
*Jump to: [Back End Stories](#back-end-stories), [Front End Stories](#front-end-stories), [Page Top](#live-project)

## Other Important Skills
This project taught me a lot about the software development industry as an individual programer and as part of a developement team implemeting agile/scrum practices. The Project consisted of a two week sprint, during this time, each student was required to attend: a sprint planning session at the start of the sprint, daily stand-up meetings at the beginning of each day, and a code retrospective review at the end of the sprint. Over the two week sprint I learned a lot about undividual strengths and weaknesses, I also had the opportunity to work under a project team environment where one's work could have a positive or negative impact on the overall project so communication and proper version control was very important.
