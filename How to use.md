##How to use

- This slide gives the various uses and applications of how to use socket.io. The code snippets in this slide have been taken from the original site of [Socket.io](http://socket.io/docs/) for better understanding purposes. The server can be made running by typing 'node app.js' in the node-js command prompt. The index.html can be checked on a browser.

- First install the socket.io software from the terminal.
 - $ npm install socket.io

- Using socket.io with Node http server: This is the basic way of using Socketio in a server-client communication.

()

- Sending and receiving events:

Socket.IO helps us to emit and receive events. Besides connect, message and disconnect, we can also emit custom events:

()

- Restricting to a namespace:

If you have control over all the messages and events emitted for a particular application, using the default / namespace works. But if we want to produce code to share with others, socket.io provides a way of namespacing a socket.This has the benefit of multiplexing a single connection. Instead of socket.io using two WebSocket connections, it will use only one.

()

- Sending and getting data (acknowledgements)

When we want to recieve an acknowledgement from the reciever after sending a message, we can get using socket.io. To do this, simply pass a function as the last parameter of '.send' or '.emit'.

()

- Broadcasting messages:

Broadcasting can be done by simply adding a broadcast flag to emit and send method calls. Broadcasting means sending a message to everyone else except for the socket that starts it.

()





[**NEXT**](https://github.com/sharathvontari/Socket.io/blob/master/Chat%20Application.md)     

[**BACK TO CONTENTS**](https://github.com/sharathvontari/Socket.io/blob/master/README.md)
