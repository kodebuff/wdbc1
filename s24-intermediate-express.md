# Rendering HTML and Templates



```javascript
// root route
app.get("/", function(req, res){
  res.render("home.ejs");
});
```

ejs (embedded JavaScript) files must be inside the "view" folder

`npm install ejs --save` 

ejs adds variables, if statements, loops, etc... inside of html.



**Adding Logic on ejs file** 

```javascript
// app.js

var express = require("express");
var app = express();

// =======================
// ROUTES
// =======================

// ROOT ROUTE
app.get("/", function(req, res){
  res.render("home.ejs");
});

app.get("/fallinlovewith/:thing", function(req, res){
  var thing = req.params.thing;
  // pass thing variable through
  res.render("love.ejs", {thingVar: thing});
});

app.get("/posts", function(req, res){
  var posts = [
    {title: "Post 1", author: "Susy"}, 
    {title: "My adorable pet bunny", author: "Charlie"}, 
    {title: "Can you believe this pomsky?", author: "Colt"} 
  ];
  res.render("posts.ejs", {posts: posts});
});

// =======================
// START SERVER
// =======================
app.listen(3000, function(){
  console.log("Server has started on port 3000...");
});
```



```embeddedjs
// home.ejs

<h1>This is the home page!</h1>

<img src="https://i2.wp.com/beebom.com/wp-content/uploads/2016/01/Reverse-Image-Search-Engines-Apps-And-Its-Uses-2016.jpg">
```



```embeddedjs
// love.ejs

<h1>You fell in love with: <%= thingVar.toUpperCase() %></h1>

<% if (thingVar.toLowerCase() === "rusty") { %>
  <p>GOOD CHOICE! RUSTY IS THE BEST!</p>
<% } else { %>
  <p>Bad choice! You should have said Rusty!</p>  
<% } %>

<p>P.S. This is the love.ejs file!</p>
```



```embeddedjs
// posts.ejs

<h1>The Posts Page</h1>

<% for (var i = 0; i < posts.length; i++) { %>
  <li>
    <%= posts[i].title %> - <strong><%= posts[i].author %></strong>
  </li>
<% } %>

<% posts.forEach(function(post){  %>
  <li>
    <%= post.title %> - <strong><%= post.author %></strong>
  </li>
<% })  %>
```



#### **Results** 

 **root route**

![root route](/img/s24-001.jpg)

**love route** 

![love route](/img/s24-002.jpg)

**posts route** 

![posts route](/img/s24-003.jpg)



# Styles and Partials

* Include public assets
* Configure app to use ejs
* Use partials to dry up code



1. Created the `public` directory and add a stylesheet inside of it.

2. Need to declare public directory in main `app.js`  by using:

   ```javascript
   app.use(express.static("public"));
   ```

3. Tell Express that all of templates must use ejs so that we can drop the .ejs :

   ```javascript
   app.set("view engine", "ejs");
   ```

4. Created directory `partials` that includes two files, header.ejs and footer.ejs to dry up the code.

   ```embeddedjs
   <% include partials/header %>
     <some code>
   <% include partials/footer %>
   ```

   **Directory Structure:**

   ![Directory Structure](/img/s24-004.jpg)



# POST Request



* set up a **POST** route, it only triggers by POST request.

  ```javascript
  // app.js

  ...

  // ROOT ROUTE
  app.get("/", function(req, res){
    res.render("home");
  });

  // POST sending data to be added or to be used somehow on the server side.
  app.post("/addfriend", function(req, res){
    // get newFriend name
    var newFriend = req.body.newfriend;
    
    //save newFriend to friends array
    friends.push(newFriend);
    
    //go back to friends list
    res.redirect("/friends");
  });

  ...
  ```

* Added form to /friends route

  ```javascript
  // friends.ejs

  <h1>Friends List goes here!!!</h1>

  <% friends.forEach(function(friend){ %>
    <li><%= friend %></li>
  <% }); %>

  <form action="/addfriend" method="POST">
    <input type="text" name="newfriend" placeholder="name">
    <button>Add New Friend</button>
  </form>
  ```

* Extracting data like newfriend from form is made possible by `body-parser` package. It is used to extract data from the body and turn it into javascript object, specifically in this case, app needs to extract newfriend data for the app to add new friend to the friends list. Install it by using `npm  body-parser --save`  and define it on the app.js:

  ```javascript
  // app.js

  ...

  var express = require("express");
  var app = express();

  var bodyParser = require("body-parser");
  app.use(bodyParser.urlencoded({extended: true}));

  // ejs thingy
  app.set("view engine", "ejs");

  ...
  ```









