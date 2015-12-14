Get Started: Chat application
In this guide we’ll create a basic chat application. It requires almost no basic prior knowledge of Node.JS or Socket.IO, so it’s ideal for users of all knowledge levels.
Introduction
Writing a chat application with popular web applications stacks like LAMP (PHP) has traditionally been very hard. It involves polling the server for changes, keeping track of timestamps, and it’s a lot slower than it should be.
Sockets have traditionally been the solution around which most realtime chat systems are architected, providing a bi-directional communication channel between a client and a server.
This means that the server can push messages to clients. Whenever you write a chat message, the idea is that the server will get it and push it to all other connected clients.
The web framework
The first goal is to setup a simple HTML webpage that serves out a form and a list of messages. We’re going to use the Node.JS web framework express to this end. Make sure Node.JS is installed.
First let’s create a package.json manifest file that describes our project. I recommend you place it in a dedicated empty directory (I’ll call mine chat-example).
{
  "name": "socket-chat-example",
  "version": "0.0.1",
  "description": "my first socket.io app",
  "dependencies": {}
}
Now, in order to easily populate the dependencies with the things we need, we’ll use npm install --save:
npm install --save express@4.10.2
Now that express is installed we can create an index.js file that will setup our application.
var app = require('express')();
var http = require('http').Server(app);

app.get('/', function(req, res){
  res.send('<h1>Hello world</h1>');
});

http.listen(3000, function(){
  console.log('listening on *:3000');
});
This translates into the following:
1.	Express initializes app to be a function handler that you can supply to an HTTP server (as seen in line 2).
2.	We define a route handler / that gets called when we hit our website home.
3.	We make the http server listen on port 3000.
If you run node index.js you should see the following:
 
And if you point your browser to http://localhost:3000:
 
Serving HTML
So far in index.js we’re calling res.send and pass it a HTML string. Our code would look very confusing if we just placed our entire application’s HTML there. Instead, we’re going to create a index.html file and serve it.
Let’s refactor our route handler to use sendFile instead:
app.get('/', function(req, res){
  res.sendFile(__dirname + '/index.html');
});
And populate index.html with the following:
<!doctype html>
<html>
  <head>
    <title>Socket.IO chat</title>
    <style>
      * { margin: 0; padding: 0; box-sizing: border-box; }
      body { font: 13px Helvetica, Arial; }
      form { background: #000; padding: 3px; position: fixed; bottom: 0; width: 100%; }
      form input { border: 0; padding: 10px; width: 90%; margin-right: .5%; }
      form button { width: 9%; background: rgb(130, 224, 255); border: none; padding: 10px; }
      #messages { list-style-type: none; margin: 0; padding: 0; }
      #messages li { padding: 5px 10px; }
      #messages li:nth-child(odd) { background: #eee; }
    </style>
  </head>
  <body>
    <ul id="messages"></ul>
    <form action="">
      <input id="m" autocomplete="off" /><button>Send</button>
    </form>
  </body>
</html>
If you restart the process (by hitting Control+C and running node index again) and refresh the page it should look like this:
 
Integrating Socket.IO
Socket.IO is composed of two parts:
•	A server that integrates with (or mounts on) the Node.JS HTTP Server: socket.io
•	A client library that loads on the browser side: socket.io-client
During development, socket.io serves the client automatically for us, as we’ll see, so for now we only have to install one module:
npm install --save socket.io
That will install the module and add the dependency to package.json. Now let’s edit index.js to add it:
var app = require('express')();
var http = require('http').Server(app);
var io = require('socket.io')(http);

app.get('/', function(req, res){
  res.sendfile('index.html');
});

io.on('connection', function(socket){
  console.log('a user connected');
});

http.listen(3000, function(){
  console.log('listening on *:3000');
});
Notice that I initialize a new instance of socket.io by passing the http (the HTTP server) object. Then I listen on theconnection event for incoming sockets, and I log it to the console.
Now in index.html I add the following snippet before the </body>:
<script src="/socket.io/socket.io.js"></script>
<script>
  var socket = io();
</script>
That’s all it takes to load the socket.io-client, which exposes a io global, and then connect.
Notice that I’m not specifying any URL when I call io(), since it defaults to trying to connect to the host that serves the page.
If you now reload the server and the website you should see the console print “a user connected”.
Try opening several tabs, and you’ll see several messages:
 

Emitting events
The main idea behind Socket.IO is that you can send and receive any events you want, with any data you want. Any objects that can be encoded as JSON will do, and binary data is supported too.
Let’s make it so that when the user types in a message, the server gets it as a chat message event. The scripts section inindex.html should now look as follows:
<script src="https://cdn.socket.io/socket.io-1.2.0.js"></script>
<script src="http://code.jquery.com/jquery-1.11.1.js"></script>
<script>
  var socket = io();
  $('form').submit(function(){
    socket.emit('chat message', $('#m').val());
    $('#m').val('');
    return false;
  });
</script>
And in index.js we print out the chat message event:
io.on('connection', function(socket){
  socket.on('chat message', function(msg){
    console.log('message: ' + msg);
  });
});




[**NEXT**](https://github.com/sharathvontari/Socket.io/blob/master/Other%20Applications.md)     

[**BACK TO CONTENTS**](https://github.com/sharathvontari/Socket.io/blob/master/README.md)

