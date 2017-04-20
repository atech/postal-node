# Postal for Node

This library helps you send e-mails through [Postal](https://github.com/atech/postal) in Node and above.

## Installation

Install the library using [NPM](https://www.npmjs.com/):

```
$ npm install postal --save
```

## Usage

Sending an email is very simple. Just follow the example below. Before you can begin, you'll
need to login to our web interface and generate a new API credential.

```javascript
// Include the Postal library
var Postal = require('postal');

// Create a new Postal client using the server key you generate in our web interface
var client = new Postal.Client('https://postal.yourdomain.com', 'your-api-key');

// Create a new message
var message = new Postal.SendMessage(client);

// Add some recipients
message.to('john@example.com');
message.to('mary@example.com');
message.cc('mike@example.com');
message.bcc('secret@awesomeapp.com');

// Specify who the message should be from. This must be from a verified domain
// on your mail server.
message.from('test@test.postal.io');

// Set the subejct
message.subject('Hi there!');

// Set the content for the e-mail
message.plainBody('Hello world!');
message.htmlBody('<p>Hello world!</p>');

// Add any custom headers
message.header('X-PHP-Test', 'value');

// Attach any files
message.attach('textmessage.txt', 'text/plain', 'Hello world!');

// Send the message and get the result
message.send().then(function (result) {
  var recipients = result.recipients();
  // Loop through each of the recipients to get the message ID
  for (var email in recipients) {
    var message = recipients[email];
    console.log(message.id());    // Logs the message ID
    console.log(message.token()); // Logs the message's token
  }
}).catch(function (error) {
  // Do something with the error
  console.log(error.code);
  console.log(error.message);
});
```
