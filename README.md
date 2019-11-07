# l17-tcp-server

# LAB - 

## Project Name

### Author: Student/Group Name

### Links and Resources
* [submission PR](http://xyz.com)
* [travis](http://xyz.com)
* [back-end](http://xyz.com) (when applicable)
* [front-end](http://xyz.com) (when applicable)

#### Documentation
* [api docs](http://xyz.com) (API servers)
* [jsdoc](http://xyz.com) (Server assignments)
* [styleguide](http://xyz.com) (React assignments)

### Modules
#### `modulename.js`
##### Exported Values and Methods

###### `foo(thing) -> string`
Usage Notes or examples

###### `bar(array) -> array`
Usage Notes or examples

### Setup
#### `.env` requirements
* `PORT` - Port Number
* `MONGODB_URI` - URL to the running mongo instance/db

#### Running the app
* `npm start`
* Endpoint: `/foo/bar/`
  * Returns a JSON object with abc in it.
* Endpoint: `/bing/zing/`
  * Returns a JSON object with xyz in it.
  
#### Tests
* How do you run tests?
* What assertions were made?
* What assertions need to be / should be made?

#### UML
Link to an image of the UML for your application and response to events

*******************

# LAB: TCP Server / Message Application

Create an event driven application that "distributes" the responsibility for logging to a **separate server** via TCP , using only events to trigger logging based on activity.

## Before you begin
Refer to *Getting Started*  in the [lab submission instructions](../../../reference/submission-instructions/labs/README.md) for complete setup, configuration, deployment, and submission instructions.


## Getting Started

* `app.js` 
  * Accepts a filename as a command line parameter
  * Reads the file from the file system
  * Converts it's contents to upper case
  * Writes it back to the file system

* `server.js` 
  * Listens for connections on port 3001
  * Broadcasts out every message it hears to all connections

## Requirements

Refactor the provided application (`app.js`) using best practices for modularization, asynchronous file access, and test-ability.

Connect the application (app.js) to the server (server.js) and emit messages related to file access.  Connect a new application (logger.js) to the server and log all file activity.


### Assignment

* Refactor `app.js` to be modular, testable, and clean
  * Read/Write should be done in promises, not callbacks
  * File Reading/Writing/Uppercasing should happen in one module
    * Each operation should be in a separate function
* Alter `app.js` to connect to the running server using TCP
  * On file errors, write an error message to the socket
  * On file save, write a save message to the socket.
* Alter `server.js` to ... 
  * Parse the text it receives
  * Given a good "event" broadcast the event to all connected clients
* Create a new application called `logger.js` ...
  * Connect to the server
  * Listen for "error" and "save" events only
  * On "save", do a `console.log()` with the message
  * On "error" do a `console.error()` with the message
  
### Notes
* You will need to start your servers up in the right order so that you can visually test things out.

1. `server.js` - needs to be up so that it can accept and re-emit events
1. `logger.js` - needs to have a running server to connect to, so that it can hear events
1. `app.js` to run and have the server hear your events
  
### Stretch Goals
* Monitor, Receive only specific events
* Allow for objects/arrays as event data
* Alter the event signature to be more scalable (i.e. replace the string based "event message..." format)
* Create a new client that listens to different events
  * i.e. split out the logger into a separate error handler
  
#### Deployment
Not required for this assignment

### Testing
* Write tests around all of your **units**
* Test event handlers (not events themselves)
* Use spies to help testing your logger methods (assert that console.log was called right)


## Assignment Submission Instructions
Refer to the the [lab submission instructions](../../../reference/submission-instructions/labs/README.md) for the complete lab submission process and expectations
