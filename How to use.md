##How to use

- This slide gives the various uses and applications of how to use socket.io. The code snippets in this slide have been taken from the original site of [Socket.io](http://socket.io/docs/) for better understanding purposes.

- First install the socket.io software from the terminal.
 - $ npm install socket.io

 - Using socket.io with Node http server

Server (app.js)

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


 - Client (index.html)

<script src="/socket.io/socket.io.js"></script>
<script>
  var socket = io('http://localhost');
  socket.on('news', function (data) {
    console.log(data);
    socket.emit('my other event', { my: 'data' });
  });
</script>

 - Using socket.io with Express 3/4 Framework

Server (app.js)

var app = require('express')();
var server = require('http').Server(app);
var io = require('socket.io')(server);

server.listen(8080);

app.get('/', function (req, res) {
  res.sendfile(__dirname + '/index.html');
});

io.on('connection', function (socket) {
  socket.emit('news', { hello: 'world' });
  socket.on('my other event', function (data) {
    console.log(data);
  });
});

 - Client (index.html)

<script src="/socket.io/socket.io.js"></script>
<script>
  var socket = io.connect('http://localhost');
  socket.on('news', function (data) {
    console.log(data);
    socket.emit('my other event', { my: 'data' });
  });
</script>

 - Using socket.io with the Express Framework

- Server (app.js)

var app = require('express').createServer();
var io = require('socket.io')(app);

app.listen(8080);

app.get('/', function (req, res) {
  res.sendfile(__dirname + '/index.html');
});

io.on('connection', function (socket) {
  socket.emit('news', { hello: 'world' });
  socket.on('my other event', function (data) {
    console.log(data);
  });
});

 - Client (index.html)
 
<script src="/socket.io/socket.io.js"></script>
<script>
  var socket = io.connect('http://localhost');
  socket.on('news', function (data) {
    console.log(data);
    socket.emit('my other event', { my: 'data' });
  });
</script>

- Sending and receiving events
Socket.IO allows you to emit and receive custom events. Besides connect, message and disconnect, you can emit custom events:
Server
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

Restricting yourself to a namespace
If you have control over all the messages and events emitted for a particular application, using the default / namespace works. If you want to leverage 3rd-party code, or produce code to share with others, socket.io provides a way of namespacing a socket.
This has the benefit of multiplexing a single connection. Instead of socket.io using two WebSocket connections, it’ll use one.
Server (app.js)
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

Sending and getting data (acknowledgements)
Sometimes, you might want to get a callback when the client confirmed the message reception.
To do this, simply pass a function as the last parameter of .send or .emit. What’s more, when you use .emit, the acknowledgement is done by you, which means you can also pass data along:

Server (app.js)
var io = require('socket.io')(80);

io.on('connection', function (socket) {
  socket.on('ferret', function (name, fn) {
    fn('woot');
  });
});

Client (index.html)
<script>
  var socket = io(); // TIP: io() with no args does auto-discovery
  socket.on('connect', function () { // TIP: you can avoid listening on `connect` and listen on events directly too!
    socket.emit('ferret', 'tobi', function (data) {
      console.log(data); // data will be 'woot'
    });
  });
</script>

Broadcasting messages
To broadcast, simply add a broadcast flag to emit and send method calls. Broadcasting means sending a message to everyone else except for the socket that starts it.
Server
var io = require('socket.io')(80);

io.on('connection', function (socket) {
  socket.broadcast.emit('user connected');
});









[**NEXT**](https://github.com/sharathvontari/Socket.io/blob/master/Chat%20Application.md)     

[**BACK TO CONTENTS**](https://github.com/sharathvontari/Socket.io/blob/master/README.md)
