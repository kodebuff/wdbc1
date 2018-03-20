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

