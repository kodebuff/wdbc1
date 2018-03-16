# YELP BASICS

**Creating YelpCamp v1:**

* Add Landing page (you can get camp images at http://photosforclass.com/search/camping)
* Add Campgrounds Page that lists all campgrounds
* Each Campground has:
  * Name
  * Image
* Create our header and footer partials
* Add in bootstrap
* Setup new Campground POST route
* Add in body-parser
* Setup route to show form
* Add basic unstyled form
* Add a better header/title
* Make campgrounds display in a grid









**Stuffs to do:**

* create json package `npm init` 

* install express ejs `npm install express ejs --save` 

* create `app.js` file

* test root route if working

* create `views` directory

* create `landing.ejs` file inside `views` directory

* create campgrounds route

* create campgrounds array (for the mean time)

* display each campground in campgrounds page

* create `partials` directory inside `views` directory

* create `header.ejs` and `footer.ejs` inside `partials` directory

* insert `<% include partials/header %>` and `<% include partials/footer %>` in `landing.ejs` and `campground.ejs` files

* add bootstrap on header.ejs

  `<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">`

* add POST route with the same route name as `/campgrounds` for REST purposes and naming conventions. 

  * `app.get("/campgrounds", ...` as a **get**, should show all campgrounds
  * `app.post("/campgrounds", ...` as a **post**, where you can create a new campground
  * `app.get("/campgrounds/new", ...` as a **get**, should show the form that will send to campgrounds **post**.  

* install `body-parser` package: `npm install body-parser --save` 

* add `var bodyParser = require("body-parser");` and 

  `app.use(bodyParser.urlencoded({extended: true}));` in app.js to use body-parser and turn data into js objects.

* add `app.get("/campgrounds/new"` route

* create  `new.ejs` file and add form for name, image and submit button

* modify `app.post("/campgrounds", ...` post route:

  ```javascript
  app.post("/campgrounds", function(req, res){
    // get data from form and add to campgrounds array
    var name = req.body.name;
    var image = req.body.image;
    // create new campground object
    var newCampground = {name: name, image: image};
    // save new campground object to campgrounds array
    campgrounds.push(newCampground);
    // redirect back to campgrounds page (GET route)
    res.redirect("/campgrounds");
  });
  ```




**Codes:** 

```javascript
// app.js

var express = require("express");
var app = express();
app.set("view engine", "ejs");

 // ========================
// ROUTES
// ========================

// root route
app.get("/", function(req, res){
  res.render("landing");
}); 

// campgrounds route
app.get("/campgrounds", function(req, res){
  
  // set up campgrounds array temporarily to run some data
  var campgrounds = [
    {name: "Sapang Palay", image: "https://pixabay.com/get/e136b80728f31c22d2524518b7444795ea76e5d004b0144394f1c471a0e9b4_340.jpg"},
    {name: "Pulong Buhangin", image: "https://pixabay.com/get/e83db50a21f4073ed1584d05fb1d4e97e07ee3d21cac104497f1c07cafeab1b9_340.jpg"},
    {name: "Biak Na Bato", image: "https://farm8.staticflickr.com/7296/28070862692_32f82c02ba.jpg"},
  ];
  res.render("campgrounds", {campgrounds:campgrounds});
});

// ========================
// START SERVER
// ========================
app.listen(3000, function(){
  console.log("YelpCamp Server has started at port 3000...");
});
```

```ejs
<!== landing.ejs ==>

<h1>Landing Page</h1>

<p>Welcome to YelpCamp!</p>

<a href="/campgrounds">View All Campgrounds</a>
```

```ejs
<!== campgrounds.ejs ==>

<h1>Camp Grounds</h1>

<% campgrounds.forEach(function(campground){ %>
  <div>
    <h4><%= campground.name %></h4>
    <img src="<%= campground.image %>">
  </div>   
<% }) %>
```

