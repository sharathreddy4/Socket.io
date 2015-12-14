##How to use

- This slide gives the various uses and applications of how to use socket.io. The code snippets in this slide have been taken from the original site of [Socket.io](http://socket.io/docs/) for better understanding purposes.

- First install the socket.io software from the terminal.
 - $ npm install socket.io

- Using socket.io with Node http server: This is the basic way of using Socketio in a server-client communication.

-->Server (server.js):

var app = require('http').createServer(handler)
var io = require('socket.io')(app);
var fs = require('fs');

app.listen(8080);

function handler (req, res) {
  fs.readFile(__dirname + '/index.html',
  function (err, data) {
    if (err) {
      res.writeHead(500);
      return res.end('Error loading index.html');
    }

   res.writeHead(200);
   res.end(data);
  });
}

io.on('connection', function (socket) {
  socket.emit('news', { hello: 'world' });
  socket.on('my other event', function (data) {
    console.log(data);
  });
});


 - Client (client.html)

<script src="/socket.io/socket.io.js"></script>
<script>
  var socket = io('http://localhost');
  socket.on('news', function (data) {
    console.log(data);
    socket.emit('my other event', { my: 'data' });
  });
</script>

 
- Sending and receiving events:

Socket.IO helps us to emit and receive events. Besides connect, message and disconnect, we can also emit custom events:

-->Server:
// note, io(<port>) will create a http server for you
var io = require('socket.io')(80);

io.on('connection', function (socket) {
  io.emit('this', { will: 'be received by everyone'});

  socket.on('private message', function (from, msg) {
    console.log('I received a private message by ', from, ' saying ', msg);
  });

  socket.on('disconnect', function () {
    io.emit('user disconnected');
  });
});

- Restricting to a namespace:

If you have control over all the messages and events emitted for a particular application, using the default / namespace works. But if we want to produce code to share with others, socket.io provides a way of namespacing a socket.This has the benefit of multiplexing a single connection. Instead of socket.io using two WebSocket connections, it will use only one.

-->Server (server.js):

var io = require('socket.io')(80);
var chat = io
  .of('/chat')
  .on('connection', function (socket) {
    socket.emit('a message', {
        that: 'only'
      , '/chat': 'will get'
    });
    chat.emit('a message', {
        everyone: 'in'
      , '/chat': 'will get'
    });
  });

var news = io
  .of('/news')
  .on('connection', function (socket) {
    socket.emit('item', { news: 'item' });
  });

- Sending and getting data (acknowledgements)

When we want to recieve an acknowledgement from the reciever after sending a message, we can get using socket.io. To do this, simply pass a function as the last parameter of '.send' or '.emit'.

-->Server (server.js):

var io = require('socket.io')(8080);

io.on('connection', function (socket) {
  socket.on('ferret', function (name, fn) {
    fn('woot');
  });
});

-->Client (client.html):

<script>
  var socket = io(); // TIP: io() with no args does auto-discovery
  socket.on('connect', function () { // TIP: you can avoid listening on `connect` and listen on events directly too!
    socket.emit('ferret', 'sharath', function (data) {
      console.log(data); // data will be 'woot'
    });
  });
</script>

- Broadcasting messages:

Broadcasting can be done by simply adding a broadcast flag to emit and send method calls. Broadcasting means sending a message to everyone else except for the socket that starts it.

-->Server

var io = require('socket.io')(80);

io.on('connection', function (socket) {
  socket.broadcast.emit('user connected');
});





[**NEXT**](https://github.com/sharathvontari/Socket.io/blob/master/Chat%20Application.md)     

[**BACK TO CONTENTS**](https://github.com/sharathvontari/Socket.io/blob/master/README.md)
