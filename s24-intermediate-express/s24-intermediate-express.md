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



