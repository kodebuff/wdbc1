# RESTFUL BLOG APP

* Create new folder `restfulBlogApp`. 

* Inside `restfulBlogApp`, create package.json: `npm init`.

* Install packages: `npm install express mongoose body-parser --save`.

* Create `app.js` file.

* Declare and set up the usual vars, settings, and mongodb connections.

  ```javascript
  // app.js

  // declare variables
  var express   = require("express"),
  bodyParser    = require("body-parser"),
  mongoose      = require("mongoose"),
  app           = express();

  // connect to mongoDB and create/use restful_blog_app db
  mongoose.connect("mongodb://localhost/restful_blog_app");

  // APP CONFIG
  app.set("view engine", "ejs");  //  ejs
  app.use(express.static("public"));  // for views directory to recognize
  app.use(bodyParser.urlencoded({extended: true})); // bodyParser
  ```

* Set root route and server (and test site if running properly).

  ```javascript
  // =============================================
  // RESTFUL ROUTES
  // =============================================

  // INDEX ROUTE
  app.get("/", function(req, res){
    res.send("THIS IS THE INDEX ROUTE PAGE!");
  });

  // =============================================
  // START SERVER
  // =============================================
  app.listen(3000, function(){
    console.log("restfulBlogApp Server has started at port 3000...");
  });
  ```

* Set schema (before routes):

  ```javascript
  // MONGOOSE/MODEL CONFIG
  var blogSchema = new mongoose.Schema({
    title: String,
    image: String,
    body: String,
    created: {type: Date, default: Date.now} //this will get the 
  });

  var Blog = mongoose.model("Blog", blogSchema); 
  ```




Source Code:

```javascript
// app.js

// declare variables
var express   = require("express"),
bodyParser    = require("body-parser"),
mongoose      = require("mongoose"),
app           = express();

// connect mongoDB and create/use restful_blog_app db
mongoose.connect("mongodb://localhost/restful_blog_app");

// APP CONFIG
app.set("view engine", "ejs");  //  ejs
app.use(express.static("public"));  // for views directory to recognize
app.use(bodyParser.urlencoded({extended: true})); // bodyParser

// MONGOOSE/MODEL CONFIG
var blogSchema = new mongoose.Schema({
  title: String,
  image: String,
  body: String,
  created: {type: Date, default: Date.now} //this will get the default date
});

var Blog = mongoose.model("Blog", blogSchema);

// // TEMPORARILY CREATE BLOG
// Blog.create(
//   {
//     title: "Test Blog",
//     image: "https://pixabay.com/get/ea37b2092df6023ed1584d05fb1d4e97e07ee3d21cac104497f1c47aa5e4b3bb_340.jpg",
//     body: "test body",
// });

// =============================================
// RESTFUL ROUTES
// =============================================

// ROOT ROUTE
app.get("/", function(req, res){
  // res.send("THIS IS THE ROOT ROUTE PAGE!");
  // redirect root route to index route
  res.redirect("/blogs");
});

// INDEX ROUTE
app.get("/blogs", function(req, res){
  
  Blog.find({}, function(err, blogs){
    if (err) {
      console.log(err);
    } else {
      res.render("index", {blogs: blogs});
    }
  });  
});



// =============================================
// START SERVER
// =============================================
app.listen(3000, function(){
  console.log("restfulBlogApp Server has started at port 3000...");
});
```

```embeddedjs
<!-- index.ejs -->

<% include ./partials/header %>

<h1>INDEX PAGE!</h1>

<% blogs.forEach(function(blog){ %>
  <div>
    <h2><%= blog.title %></h2>
    <img src="<%= blog.image %>">
    <span><%= blog.created %></span>
    <p><%= blog.body %></p>
  </div>
<% }) %>

<% include ./partials/footer %>
```

```embeddedjs
<!-- header.ejs -->

<!DOCTYPE html>
<html>
<head>
  <title>Restful Blog App</title>
  <link rel="stylesheet" type="text/css" href="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.3.1/semantic.min.css" >
  <link rel="stylesheet" type="text/css" href="stylesheets/app.css" >
</head>
<body>
  <div class="ui fixed inverted menu">
    <div class="ui container">
      <div class="header item"><i class="code icon"></i>Blog Site</div>
      <a href="/" class="item">Home</a>
      <a href="/blogs/new" class="item">New Post</a>
    </div>
  </div>
```

```embeddedjs
<!-- footer.ejs -->

</body>
</html>
```

```css
/* app.css */

i.icon {
  font-size: 2em;
}
```





