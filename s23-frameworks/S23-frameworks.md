# Intro to Express

**What is a framework? How does it differ from a library?** 

* The defining difference between a library and a framework is Inversion of Control. When you call a library, you are in control. But with a framework, the control is inverted: the framework calls you. 
* Basically, all the control flow is already in the framework, and there's just a bunch of predefined white spots that you can fill out with your code. 
* A library on the other hand is a collection of functionality that you can call.



**What is Express?** 

* It's a web development framework.



**Why are we using Express?** 

* Most popular Node JS framework, there's lots of tutorials.
* Lightweight framework. It doesn't hide things from you.



**Installing Express** 

`npm install express --save` 



# NPM init and package.json

- Use of `--save` flag to install packages
  - saving the installed NPM package to dependencies section of package.json
- What package.json file does
  - json stands for JavaScript object notation, a way of formatting text in a file to represent structure. A file that contains all the metadata about a particular application. It holds metadata relevant to a specific project.
  - json is like a recipe for the ingredients that are needed for a specific package or library. Rather than sending the contents of all individual package (dependencies), we just send package.json instead.
- Use of `npm init` to create a new package.json
  - initializes package.json to set metadata.



**Basic routing** 

*Routing* refers to determining how an application responds to a client request to a particular endpoint, which is a URI (or path) and a specific HTTP request method (GET, POST, and so on).

Each route can have one or more handler functions, which are executed when the route is matched.

Route definition takes the following structure: `app.METHOD(PATH, HANDLER)`

Where:

- `app` is an instance of `express`.
- `METHOD` is an HTTP request method, in lowercase.
- `PATH` is a path on the server.
- `HANDLER` is the function executed when the route is matched.

The following examples illustrate defining simple routes. Respond with `Hello World!` on the homepage:

```javascript
app.get('/', function (req, res) {
  res.send('Hello World!')
});
```

Respond to POST request on the root route (`/`), the application’s home page:

```javascript
app.post('/', function (req, res) {
  res.send('Got a POST request')
});
```

Respond to a PUT request to the `/user` route:

```javascript
app.put('/user', function (req, res) {
  res.send('Got a PUT request at /user')
});
```

Respond to a DELETE request to the `/user` route:

```javascript
app.delete('/user', function (req, res) {
  res.send('Got a DELETE request at /user')
});
```

Reference: [Express Basic Routing](https://expressjs.com/en/starter/basic-routing.html)



**A simple example of "Hello World" Express application:** 

```javascript
var express = require('express');
var app = express();

// =====================================
// ROUTES
// =====================================
app.get('/', function (req, res) {
  res.send('Hello World!')
});

// =====================================
// START SERVER
// =====================================
app.listen(3000, function(){
  console.log("Server has started on port 3000...");
});
```



# MORE ROUTING

**Order of Routes** 

* Order of routes MATTER!
* The first route that matches a given request is the only route that will be run.



**The `*` Route Matcher** 

```javascript
// All routes THAT ARE NOT DEFINED Will land in this page. THIS IS USEFUL FOR ERROR LANDING PAGE.
// BUT DO NOT PUT THIS AT THE FIRST ROUTE AS IT WILL NOT EXECUTE EVEN THE DEFINED ROUTES.
// ORDER OF ROUTES MATTER!
app.get("*", function(req, res){
  res.send("YOU ARE A STAR!!!");
});
```



**Route Parameters** 

* Sometimes called route variables or path variables.

* Used to define a pattern in a route.

  ```javascript
  // ROUTE PARAMETER EXAMPLE
  // : is the indicator for route variables
  app.get("/r/:subredditName", function(req, res){
    res.send("WELCOME TO A SUBREDDIT!");
  });

  // ANOTHER EXAMPLE
  app.get("/r/:subredditName/comments/:id/:title", function(req, res){
    res.send("WELCOME TO THE COMMENTS PAGE!");
  });

  // PERSONALISING THE PAGE BY PUTTING THE subredditName
  app.get("/r/:subredditName", function(req, res){
    // console.log will capture the req.params to view the route variables.
    // console.log(req.params);
    var subreddit = req.params.subredditName;
    res.send("WELCOME TO THE " + subreddit.toUpperCase() + " SUBREDDIT!");
  });
  ```



**EXPRESS ROUTING ASSIGNMENT**

```javascript
1. Create a brand new Express app from scratch.
2. Create a package.json using npm init and add express dependency.
3. In your main app.js files, add 3 different routes.

Visiting "/" should print "Hi there, welcome to my assignment!"
================================================================
Visiting "/speak/pig" should print "The pig says 'Oink'"
Visiting "/speak/cow" should print "The cow says 'Moo'"
Visiting "/speak/dog" should print "The dog says 'Woof Woof!'"
================================================================
Visiting "/repeat/hello/3" should print "hello hello hello"
Visiting "/repeat/hello/5" should print "hello hello hello hello hello"
Visiting "/repeat/blah/2" should print "blah blah"
================================================================
If a user visits any other route, print:
"Sorry, page not found... What are you doing with your life?"

```

