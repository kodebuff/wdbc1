# RESTFUL ROUTING 

**REST** 

* Representational State Transfer.

* A mapping between HTTP routes and CRUD.

* Pattern of defining our routes.

  ​

**Table of all 7 RESTful routes**

| Name    | Path (example) | HTTP Verb | Purpose                                          | Mongoose Method         |
| ------- | -------------- | --------- | :----------------------------------------------- | ----------------------- |
| INDEX   | /dogs          | GET       | List all dogs                                    | Dog.find()              |
| NEW     | /dogs/new      | GET       | Show new dog form                                | N/A                     |
| CREATE  | /dogs          | POST      | Create new dog, then redirect somewhere          | Dog.Create()            |
| SHOW    | /dogs/:id      | GET       | Show info about one specific dog                 | Dog.findById()          |
| EDIT    | /dogs/:id/edit | GET       | Show edit form for one dog                       | Dog.findById()          |
| UPDATE  | /dogs/:id      | PUT       | Update a particular dog, then redirect somewhere | Dog.findByIdAndUpdate() |
| DESTROY | /dogs/:id      | DELETE    | Delete a particular dog, then redirect somewhere | Dog.findByIdAndRemove() |



# RESTFUL BLOG APP

### INDEX ROUTE 

* use of semantic-ui as CSS framework (semantic-ui.com)

* create app-directory, then `npm init` 

* install packages `npm install express ejs mongoose body-parser --save` 

* create `app.js`  

* create variables to use:

  ```javascript
  // app.js

  // declare variables
  var express   = require("express"),
  bodyParser    = require("body-parser"),
  mongoose      = require("mongoose"),
  app           = express();
  ```

* create a connection and db with mongoDB:

  ```javascript
  // app.js

  // connect mongoDB and create (if not existing) OR use (if existing) restful_blog_app db
  mongoose.connect("mongodb://localhost/restful_blog_app");
  ```

* add code for app config:

  ```javascript
  // app.js

  // APP CONFIG
  app.set("view engine", "ejs");  //  ejs
  app.use(express.static("public"));  // for views directory to recognize
  app.use(bodyParser.urlencoded({extended: true})); // bodyParser
  ```

* add server port to start server: (and test if running, `node app.js` )

  ```javascript
  // app.js

  // =============================================
  // START SERVER
  // =============================================
  app.listen(3000, function(){
    console.log("restfulBlogApp Server has started at port 3000...");
  });
  ```

* create db schema at the top of APP CONFIG:

  ```javascript
  // app.js

  // MONGOOSE/MODEL CONFIG
  var blogSchema = new mongoose.Schema({
    title: String,
    image: String,
    body: String,
    created: {type: Date, default: Date.now} //this will get the default date
  });

  var Blog = mongoose.model("Blog", blogSchema); // compile schema to Blog
  ```

* after MONGOOSE/MODEL CONFIG, create a sample blog for testing: (this must be run once and must be commented out or removed after creating)

  ```javascript
  // app.js

  // TEMPORARILY CREATE BLOG
  Blog.create(
    {
      title: "Test Blog",
      image: "https://pixabay.com/get/ea37b2092df6023ed1584d05fb1d4e97e07ee3d21cac104497f1c47aa5e4b3bb_340.jpg",
      body: "test body",
      // leave created as it automatically creates date (Date.now function)
  });
  ```

* add INDEX ROUTE: (and redirect ROOT ROUTE to INDEX ROUTE)

  ```javascript
  // app.js

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

  // make sure to have an index.ejs file inside views folder
  // Blog.find({}, function(err, blogs)... --> will find all the blogs in MongoDB and save it under blogs
  // res.render("index", {blogs: blogs}); --> will pass in all data from blogs (2nd) to blogs (1st)
  ```

* ROOT ROUTE: (redirected to INDEX ROUTE)

  ```javascript
  // app.js

  // ROOT ROUTE
  app.get("/", function(req, res){
    // redirect root route to index route
    res.redirect("/blogs");
  });
  ```

* create `index.ejs` inside `views` folder:

  ```embeddedjs
  <!-- index.ejs -->

  <h1>INDEX PAGE!</h1>

  <% blogs.forEach(function(blog){ %>
    <div>
      <h2><%= blog.title %></h2>
      <img src="<%= blog.image %>">
      <span><%= blog.created %></span>
      <p><%= blog.body %></p>
    </div>
  <% }) %>

  <!--
    <% blogs.forEach(function(blog){ %> - loop through all blogs

    and display each blog with:
      blog title:   <h2><%= blog.title %></h2>
      blog image:   <img src="<%= blog.image %>">
      date created: <span><%= blog.created %></span>
      blog desc:    <p><%= blog.body %></p>
  -->
  ```



### ADD BASIC LAYOUT (Before NEW ROUTE)

* Add header and footer inside `views/partials` folder:

  ```embeddedjs
  <!-- header.ejs -->

  <!DOCTYPE html>
  <html>
  <head>
    <title>Restful Blog App</title>
  </head>
  <body>
   

  <!-- footer.ejs -->
    
  </body>
  </html>
  ```

* link the header and footer to index.ejs:

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


* add semantic-ui CSS framework:

  ```embeddedjs
  <!-- header.ejs -->

    <!DOCTYPE html>
    <html>
    <head>
      <title>Restful Blog App</title>
      <link rel="stylesheet" type="text/css" href="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.3.1/semantic.min.css" >
        (...)
        
    <!-- added the minified version to make web app faster -->
  ```


* add header section:

  ```embeddedjs
  <!-- header.ejs -->

  (...)

  <body>
    <div class="ui fixed inverted menu">
      <div class="ui container">
        <div class="header item"><i class="code icon"></i>Blog Site</div>
        <a href="/" class="item">Home</a>
        <a href="/blogs/new" class="item">New Post</a>
      </div>
    </div>

  (...)
  ```

* add app.css in `public\stylesheets` folder:

  ```css
  /* app.css */

  i.icon {
    font-size: 2em; /* double the size of icon relative to the parent */
  }
  ```



### NEW and CREATE ROUTE 

* add codes for NEW (will show form) and CREATE ROUTE (add created post and show in index) :

  ```javascript
  // app.js

  // after INDEX ROUTE

  // NEW ROUTE
  app.get("/blogs/new", function(req, res){
    res.render("new");
  });

  // CREATE ROUTE
  app.post("/blogs", function(req, res){
    // create blog
    // Blog.create(data, callback);
    // data is from new.ejs inputs blog[title], blog[image], blog[body]
    // which in app.post, those data is inside of req.body.blog
    Blog.create(req.body.blog, function(err, newBlog){
      if (err) {
        // console.log(err); 

        // instead of console.log, go to new
        res.render("new");
      } else {
        // redirect to INDEX ROUTE
        res.redirect("/blogs");
      }
    });
  });

  // before SERVER ROUTE
  ```

* create `new.ejs` file in `views` folder:

  ```embeddedjs
  <!-- new.ejs -->

    <% include ./partials/header %>

    <div class="ui main text container segment">
      
      <div class="ui huge header">New Blog</div>
      
      <form class="ui form" action="/blogs" method="POST">
        <div class="field">
          <label>Title</label>
          <input type="text" name="blog[title]" placeholder="title">
        </div>
        <div class="field">
          <label>Image</label>
          <input type="text" name="blog[image]" placeholder="image">
        </div>
        <div class="field">
          <label>Blog Content</label>
          <textarea name="blog[body]"></textarea>
        </div>

        <input class="ui violet basic big button" type="submit">
      </form>

    </div>

    <% include ./partials/footer %>
  ```




### SHOW ROUTE

* add code for additional links in `index.ejs` 

  ```embeddedjs
  <!--
    add this line to index.ejs after p tag for blog.body:
    <a href="/blogs/<%= blog._id %>"></a>
  -->

  <% blogs.forEach(function(blog){ %>
    <div>
      <h2><%= blog.title %></h2>
      <img src="<%= blog.image %>">
      <span><%= blog.created %></span>
      <p><%= blog.body %></p>
      <a href="/blogs/<%= blog._id %>"></a>
    </div>
  <% }) %>
  ```

* add code for SHOW ROUTE after CREATE ROUTE:

  ```javascript
  // SHOW ROUTE
  app.get("/blogs/:id", function(req, res){

    // Blog.findById(id, callbackFunction)
    // id is in req.params.id
    Blog.findById(req.params.id, function(err, foundBlog){
      if (err) {
        // go back to index page
        res.redirect("/blogs");
      } else {
        res.render("show", {blog: foundBlog});
      }
    });
  });
  ```

* create `show.ejs` in `views` folder:

  ```embeddedjs
  <!-- show.ejs -->

  <% include ./partials/header %>

  <div class="ui main text container segment">  
    <div class="ui huge header"><%= blog.title %></div>
    <div class="ui top attached">
      <div class="item">
        <img class="ui centered rounded image" src="<%= blog.image %>">
        <div class="content">
          <span><%= blog.created.toDateString() %></span>
        </div>
        <div class="description">
          <p><%= blog.body %></p>
        </div>
      </div>
    </div>  
  </div>

  <% include ./partials/footer %>
  ```



### EDIT ROUTE

* add code for EDIT ROUTE 

  ```javascript
  // EDIT ROUTE
  app.get("/blogs/:id/edit", function(req, res){
    // go to edit.ejs form
    res.render("edit");
  });
  ```

* create `edit.ejs` file in `views` folder:

  ```embeddedjs

  ```

* ​



Source Code:

```javascript
// app.js

// declare variables
var express    = require("express"),
bodyParser     = require("body-parser"),
methodOverride = require("method-override"),
mongoose       = require("mongoose"),
app            = express();

// connect mongoDB and create (if not existing) OR use (if existing) restful_blog_app db
mongoose.connect("mongodb://localhost/restful_blog_app");

// APP CONFIG
app.set("view engine", "ejs");  //  ejs
app.use(express.static("public"));  // for views directory to recognize
app.use(bodyParser.urlencoded({extended: true})); // bodyParser
app.use(methodOverride("_method")); // this will use to cheat PUT in edit.ejs

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

// ====================================
// RESTFUL ROUTES
// ====================================

// ROOT ROUTE
app.get("/", function(req, res){
  // redirect root route to index route
  res.redirect("/blogs");
});

// INDEX ROUTE
app.get("/blogs", function(req, res){  
  // find all the blogs in MongoDB and save it under blogs
  Blog.find({}, function(err, blogs){
    if (err) {
      console.log(err);
    } else {
      // pass in all data from blogs (2nd, from callback function) 
      // to blogs (1st, assigned variable to be rendered in index.ejs)
      res.render("index", {blogs: blogs});
    }
  });  
});

// NEW ROUTE
app.get("/blogs/new", function(req, res){
  // go to new.ejs form 
  res.render("new");
});

// CREATE ROUTE
app.post("/blogs", function(req, res){
  // create blog
  // Blog.create(data, callback);
  // data is from new.ejs inputs blog[title], blog[image], blog[body]
  // which in app.post, those data is inside of req.body.blog
  Blog.create(req.body.blog, function(err, newBlog){
    if (err) {
      // instead of console.log, go to new.ejs form (will create error page soon)
      res.render("new");
    } else {
      // redirect to INDEX ROUTE
      res.redirect("/blogs");
    }
  });
});

// SHOW ROUTE
app.get("/blogs/:id", function(req, res){
  // Blog.findById(id, callbackFunction)
  // id is in req.params.id
  // and save all data to foundBlog
  Blog.findById(req.params.id, function(err, foundBlog){
    if (err) {
      // go back to index route
      res.redirect("/blogs");
    } else {
      // pass in all data from foundBlog(from callback function) 
      // to blog (assigned variable to be rendered in show.ejs)
      res.render("show", {blog: foundBlog});
    }
  });
});

// EDIT ROUTE
app.get("/blogs/:id/edit", function(req, res){
  // Blog.findById(id, callbackFunction)
  // id is in req.params.id
  // and save all data to foundBlog
  Blog.findById(req.params.id, function(err, foundBlog){
    if (err) {
      // go back to index route
      res.redirect("/blogs");
    } else {
      // pass in all data from foundBlog(from callback function) 
      // to edit (assigned variable to be rendered in edit.ejs)
      res.render("edit", {blog: foundBlog});
    }
  });
});

// UPDATE ROUTE
app.put("/blogs/:id", function(req, res){
  // res.send("UPDATE ROUTE!");
  // Blog.findByIdAndUpdate(id, newData, callback);
  Blog.findByIdAndUpdate(req.params.id, req.body.blog, function(err, updatedBlog){
    if (err) {
      // go back to index route
      res.redirect("/blogs");
    } else {
      // go to SHOW ROUTE with specific blog id
      res.redirect("/blogs/" + req.params.id);
    }
  });
});

// DELETE ROUTE
app.delete("/blogs/:id", function(req, res){
  // Destroy blog
  Blog.findByIdAndRemove(req.params.id, function(err){
    if (err) {
       // go back to index route
      res.redirect("/blogs");
    } else {
      // Redirect somewhere 
      res.redirect("/blogs");
    }
  });
});

// ====================================
// START SERVER
// ====================================
app.listen(3000, function(){
  console.log("restfulBlogApp Server has started at port 3000...");
});
```

