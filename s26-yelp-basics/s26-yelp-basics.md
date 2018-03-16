# YELP BASICS

**Creating YelpCamp v1:**

* Add Landing page
* Add Campgrounds Page that lists all campgrounds
* Each Campground has:
  * Name
  * Image



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

