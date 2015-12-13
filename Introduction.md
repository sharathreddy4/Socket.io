##Introduction 

#####What is the WebSocket ?

WebSocket is a protocol for bidirectional communication of data through channels within a single TCP connection. The WebSocket protocol was set as a standard by the IETF as RFC 6455.

The WebSocket API is the method that enables asynchronous (duplex) communication between client and server.

This uses either  ws (insecure) or wss (secure) protocol and can be used by any client or server application.

The distinguishing feature of WebSocket API is that the server and client can push messages to each other at any given time (Real time data transfer).
 In AJAX technologies a request is supposed  to be made by the client, whereas WebSocket servers and clients can send each other messages. In case of  XHR, it is limited by domain whereas WebSocket API allows cross-domain messaging as well.


#####Socket.IO


Socket.IO is a library in javascript for web applications. This can be used for developing applications that require real time events like chat server etc which needs communication response from both client and the server. It is available in two forms a client-side library and a server-side library.

Socket.IO was created by Guillermo Rauch, CTO of [LearnBoost](https://www.learnboost.com) and lead scientist of LearnBoost Labs. Socket.IO uses feature detection to decide whether the connection between client and server will be established with WebSocket, AJAX long polling, Flash, etc.,helping in the creation of realtime apps.

Socket.IO uses websocket protocol to provide a bidirectional communication channel over a single connection working on TCP.

Sometimes it can be considered as a wrapper for WebSocket, but Socket.io provides many other features like broadcasting to multiple connections, client data storage etc.

Socket.io is a library for developing a customized  real-time protocol over other protocols offering real-time features. 
In case of development of any client server application model both the client and the server had to be developed using Socket.IO. Few rules of negotiation are developed such that, they do not allow other applications to connect with Socket.IO servers. Thus Socket.IO libraries should be used on both client and server side to interact with each other.
Thus [infoworld.com] (http://www.infoworld.com/article/2607757/javascript/socket-io-javascript-framework-ready-for-real-time-apps.html) defines Socket.IO as a framework for mobile and Web apps and supports bidirectional, event-based communication. This framework, offers an library (engine module) for improving reliability and supports bidirectional communication.

This library is mainly used for real-time communication.For example in a chat server if one is typing a message the other has to see that the other person is typing something. In this case there is requirement for real time response. In such cases Socket.Io can be used as It is a simple method to exchange messages between the client and the server.








[**NEXT**](https://github.com/sharathvontari/Socket.io/blob/master/How%20to%20use.md)     

[**BACK TO CONTENTS**](https://github.com/sharathvontari/Socket.io/blob/master/README.md)
