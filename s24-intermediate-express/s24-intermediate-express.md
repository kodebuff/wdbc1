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







