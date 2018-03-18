# Intro to Databases

**What is a database?** 

* A collection of information/data.
* Has an interface.



**SQL (relational) and NoSQL (non-relational)** 

* SQL is tabular and flat.
* NoSQL has no tables, has more flexible structure**.** The structure looks like JS objects.



**MongoDB** 

* NoSQL DB



**Why use it?** 

* The most popular DB now with Node
* MEN (MongoDB, Express, and Node) Stack



**Start/Stop MongoDB** 

* After configuring and installing mongod.cfg, you can use net start/stop commands in cmd/terminal.


* Make sure cmd/terminal is running in admin mode. 


* `net start MongoDB` - starts MongoDB
* `net stop MongoDB` - stops MongoDB



**First Mongo Commands:** 

* `mongod` - needs to run all the time to use mongoDB

* `mongo` - opens up the mongo shell

* `help` -  list some helpful commands

* `show dbs` - show database names

* `use <db_name>` - set current database. if database does not exist, it will create one and use it.

  * EX: use demo 

* insert - `db.dogs.insert()` WHERE:

  * db - the current database (demo)
  * dogs - collections (not existing yet)
  * insert - add data into collections (dogs)

* `show collections` - shows current collections (in this instance, dogs)

* `db.dogs.find()` - list the data inside dogs collections

  * `db.dogs.find({name: "Rusty"})` - look for a specific data with name: "Rusty"

* `db.dogs.update()` - update data with specific parameters

  * `db.dogs.update({name: "Lulu"}, {breed: "Labradoodle"})`  - this will update Lulu's breed from "Poodle" to "Labradoodle". 

    **TAKE NOTE:** This will override the data, when you run `db.dogs.find()`, you will see all the data in dogs collections except Lulu. Lulu's data was replaced from `{name: "Lulu", breed: "Poodle"}` to `{breed: "Labradoodle"}` **only**.

  * use update in this format instead, 

    `db.dogs.update({name: "Rusty"}, {$set: {name: "Tater", isCute: true}})` 

    * this will preserve Rusty's breed as Mutt but it will update its name to Tater and add new object isCute: true

* `db.dogs.remove({breed: "Labradoodle"})` - removes data with breed: Labradoodle

* CRUD

  * CREATE: `db.dogs.find({name: "Rusty", breed: "Mutt"})` 
  * READ: `db.dogs.find({name: "Rusty"})` 
  * UPDATE: ``db.dogs.update({name: "Rusty"}, {$set: {name: "Tater", isCute: true}})` 
  * DELETE: `db.dogs.remove({breed: "Labradoodle"})` 




**Mongoose** 

* Mongoose is a tool (npm) that helps us interact with MongoDB. 
* ​