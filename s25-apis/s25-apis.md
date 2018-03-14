# APIs

* Opens up the possibilities of what you can build.
* Can use data from other applications.
* Connecting with other applications (data to display map, data of latitude or longitude, weather data, ...)
* write code that uses APIs.



**Application Programming Interface** is an interface for code/computers to talk to one another.



**WEB APIs** generally communicate via HTTP

![WEB APIs](/img/s25-001.jpg)



* [IFTTT](http://www.ifttt.com) - one way to connect APIs, have a visual interface to connect APIs to do things for you.
* [programmableweb](http://www.programmableweb.com) - has 15K+ APIs. Great place to start. 



**Example iTunes API Requests:** 

![iTunes API Request](/img/s25-002.jpg)



**Data Formats:** 

![Data Formats](/img/s25-003.jpg)



* **XML** (Extended Markup Language) - syntactically similar to HTML, but it does not describe presentation like HTML does.

  ```html
  <person>
    <age>21</age>
    <name>Travis</name>
    <city>Los Angeles</city>
  </person>
  ```

* **JSON** (JavaScript Object Notation) - looks exactly like JS objects, but everything is a string

  ```javascript
  {
    "person": {
      "age": "21",
      "name": "Travis",
      "city": "Los Angeles"
    }
  }
  ```



**Making API Request using Node (Request - Simplified HTTP client)** 

* Install request package `npm install request` 
* [Request Package Github page](http://www.github.com/request/request)




**Make a simple app that prints sunset time in Hawaii** 

* install `npm request` 

* get yahoo endpoint (api) for hawaii sunset

* body is type string, parse and save it in a container `var parsedData = JSON.parse(body);` 

* output sunset time `console.log("Sunset in Hawaii is at " + parsedData["query"]["results"]["channel"]["astronomy"]["sunset"]);` 

* Code:

  ```javascript
  // hawaii_sunset.js

  var request = require('request');

  request('https://query.yahooapis.com/v1/public/yql?q=select%20astronomy.sunset%20from%20weather.forecast%20where%20woeid%20in%20(select%20woeid%20from%20geo.places(1)%20where%20text%3D%22maui%2C%20hi%22)&format=json&env=store%3A%2F%2Fdatatables.org%2Falltableswithkeys', function(error, response, body){
    if (!error && response.statusCode == 200) {

      // but body is type string
      // console.log(body);
      
      // parse body into object and save it in a container
      var parsedData = JSON.parse(body);
      
      //console.log(parsedData);
      //console.log("Sunset in Hawaii is at " + parsedData.query.results.channel.astronomy.sunset);
      console.log("Sunset in Hawaii is at " + parsedData["query"]["results"]["channel"]["astronomy"]["sunset"]);
    }
  });
  ```





**Movie App** 

* Create new folder `MovieSearchApp` 
* Create package.json `npm init` 
* Install express, ejs, and request packages `npm install --save express ejs request` 
* Go to omdbapi.com for documentation
* ​