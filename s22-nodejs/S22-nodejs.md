# Intro to Node JS

**What is Node?** 

- Node is a way to write JavaScript code on the server side.

**Why are we learning it?** 

- It's popular.
- JavaScript!



**Using Node** 

* Interact with Node Console.
  * Make sure Node JS is installed, go to terminal, type node. To exit, press ctrl + c twice.
* Run a file with Node.
  * `node <filename>`
* REPL - Read, Evaluate, Print, Loop



**NODE EXERCISES**

1. Echo Function

   * Using the command line, create a file echo.js

   * Inside the file, write a function named echo that takes 2 arguments: a string and a number.

   * It should print out the string, number number times.

   * echo("Echo!!!", 10) // should print "Echo!!!" 10 times

   * echo("Tater Tots", 3) // should print "Tater Tots" 3 times

   * Add the above to examples to the end of your file.

   * Lastly, run the contents of "echo.js" using node.

     ```javascript
     function echo(str, num) {
       for (var i = 0; i < num; i++) {
         console.log(str);
       }
     }

     // TEST
     echo("Echo!!!", 10);
     echo("Tater Tots", 3);
     ```

     type `node echo.js` on the terminal to run echo.js in node.

   ​


1. Average Grade

   * Create a new file, "grader.js"

   * In the file, define a new function named "average".

   * It should take a single parameter: an array of test scores (all umbers)

   * It should return the average score in the array, rounded to the nearest whole number.

   * var scores = [90, 98, 89, 100, 100, 86, 94];

   * average(scores) // should return 94

   * var scores2 = [40, 65, 77, 82, 54, 73, 63, 95, 49];

   * average(scores2) // should return 68

     ```javascript
     var scores = [90, 98, 89, 100, 100, 86, 94];
     var scores2 = [40, 65, 77, 82, 80, 54, 73, 63, 95, 49];

     function average(arrScores) {
       var totalScore = 0;
       
       // my solution to sum up all grades in array
       // for (var i = 0; i < arrScores.length; i++) {
       //   totalScore += arrScores[i];
       // }

       // add all scores together
       arrScores.forEach(function(score) {
         totalScore += score;
       });

       var avg = totalScore / arrScores.length;
       return Math.round(avg);
     }

     console.log(average(scores));
     console.log(average(scores2));
     ```

     type `node grader.js` on the terminal to run echo.js in node.




# Intro to NPM

**Define NPM** 

* NPM (Node Package Manager) is the package manager of JavaScript. Packages (kinda JS version of libraries) are codes that someone else has written that we can include and add to our own project.
* to install a package, type `npm install <package-name>` in terminal.

**Why NPM is awesome?** 

* NPM is easy to use.
* Centralized repositories of different packages.




**Installing and Using Packages**

* Use `npm install` to install a package
* Use `require()` to include a package



**NPM EXERCISE:** 

* Create a new directory named "MyShop"
* Add a file named "listProducts.js"
* Install the "Faker" package
* Read the Faker docs and figure out how it works
* Use Faker to print out 10 random product names and prices
* BE RESOURCEFUL! DON'T CHEAT AND FAST FORWARD!!!
* Run your file with node and make sure it works!

```javascript
var faker = require('faker');

// var randomProductName = faker.commerce.productName(); // random product name
// var randomPrice = faker.finance.amount(); // random amount;

console.log("===================");
console.log("WELCOME TO MY SHOP!");
console.log("===================");

for (var i = 0; i < 10; i++) {
  // my solution
  // console.log(randomProductName + " - $" + randomPrice); // shows 10 same items
  // console.log(faker.fake("{{commerce.productName}} - ${{finance.amount}}"));  
  
  // colt's solution
  console.log(faker.commerce.productName() + " - $" + faker.commerce.price());
}
```




