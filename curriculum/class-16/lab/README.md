# Lab - Event Driven Applications

Create an event driven "smart app"

### Before you begin
* You'll need to perform an `npm install` in this folder to have jest installed as a dependency.

## Assignment
Refactor the provided application using best practices for modularization, asynchronous file access, and test-ability.

The application currently uses a nested callback to accept a file from the user, open it, uppercase its contents, and then save it back. It throws errors on failure and logs out success messages.

The task for today is to refactor the application to use events to surface errors and completion status, while also moving away from the big un-testable callback.


### Requirements 
* The application must accept a filename as a command line parameter
  * Read the file from the file system
  * Convert it's contents to upper case
  * Write it back to the file system
* Following the write operation, report back to the user (console.log) the status
* Any and all errors must be thrown

### Implementation Details
* Ensure that every function has JSDoc Notation
* Refactor the use of callbacks for fs operations into promises
  * You can use util.promisify() to do this.
* Separate the functionality of that big callback into it's parts, so that you can run them indepedently as well as test.
  * Read in a file
  * Uppercase it's contents (stringify the buffer, upper case it, re-buffer-ize it)
  * Save back to the file.
* Rather than throwing errors and console.log() inline, fire events 
* Implement a separate event listener to "hear" and "deal" with those events
* Modularize the system
  * Create an event module that has a single event emitter instance
  * File Reading/Writing/Uppercasing should happen in one module
    * Each operation should be in a separate function
    * Read/Write should be done in promises, not callbacks
  * Subscribers to file status events should be in a separate module (maybe called "logger")
    * On a successful conversion and save-back, the logger should send a message
    * If an error happens, throw it.  

### Testing
* Write tests around all of your units
  * File Read, File Save, Uppercase
  * Mock the fs module methods so that your tests don't use actual files
* Test event handlers (not events themselves)
* Use spies to help testing your logger methods (assert that console.log was called right)

###  Documentation
Complete the README.md file included in the lab folder
