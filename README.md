# Backbone.js Todos example app using ss-couchbone

This is an example application to demonstrate how to use the [ss-couchbone](https://github.com/colinf/ss-couchbone) Socketstream Request Responder.

It's based on the [original backbone.js example](http://backbonejs.org/examples/todos/index.html) Todos application but has been modified so that, instead of using browser localstorage to save the todo list, it uses a CouchDB database at the server end over websockets. The ss-couchbone request responder is used to enable this.

## Running the example
### Create the database
You need to create a CouchDB database to store the todo list. Assuming that you already have a CouchDB instance that you can access, this is done as follows:

1. Create an empty database called **cb-todos** (you can call it something else if you prefer and then amend the relevant setup step below accordingly).
2.  Create a view on your new database with details as below. If you're not that familiar with CouchDB views, you can do this using CouchDB Futon and there is a simple writeup on this [blog page](http://blog.vicmetcalfe.com/2011/04/11/creating-views-in-couchdb-futon/). The details for the design document you should create for the view are as follows:
	* _id: "_design/views" 
	* views: see following code snippet

```javascript
{
	"testview": {
		"map": "function(doc) {emit(doc._id, doc)}"
	}
}
```
### Database connection setup
You now need to enter the connection details for the CouchDB database that you have created. The good news is that if you are running CouchDB on localhost using the default port of 5984 and have used the suggested database name of **cb-todos** as per step 1 above, then you can skip this step of database connection setup and move straight on to running the app below.

If you do need to customise the database connection details then edit the file client/code/app/app.js and search for "setup". You should see the code below:

```javascript
ss.cbone('setup', {
  host: 'http://localhost',
  port: 5984,
  cache: true,
  raw: false}, 'cb-todos');
```
Edit the values for your database host/port accordingly and change the name of the database from cb-todos if you have chosen your own.
### Run the app
Finally, to start your app use the following standard command from the couchbone-todos directory:

	node app.js
And then visit the app at:

	http://localhost:3000
where you should be able to use the Todos example application in exactly the same way as the original.
***