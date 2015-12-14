##Sample Chat Application

- In this slide we are going to develop a simple chat application using node.js and socket.io.

Writing a chat application with other web applications such as PHP is difficult because it involves polling the server for changes, keeping track of timestamps, and it is also very slow. As asolution to this Sockets came up with better realtime chat systems which  providing a bi-directional communication channel between a client and a server.

- Setup:
1.The first thing is to setup a simple HTML webpage that serves out a form and a list of messages. We’re going to use the Node.JS web framework. So we should make sure that Node.JS is installed.

2.Let’s create a package.json manifest file that describes our project. 

()

3.Now, we will install express framework onto node.js.

npm install --save express@4.10.2

4.Now that express is installed we can create an index.js file that will setup our application.

()

This file helps us do the the following:
1.	Express initializes app to be a function handler that you can supply to an HTTP server.
2.	We define a route handler / that gets called when we hit our website home.
3.	We make the http server listen on port 8097.

5.Now if we run node index.js, we can see the following output on the terminal:

()
 
And if we type http://localhost:8097, we should it as below:

()

 
6. Creating HTML file

So far in index.js we’re calling res.send and pass it a HTML string. Our code would look very confusing if we further modified it by adding various features of our entire application’s HTML there. Instead, we’re going to create a index.html.

()

If you restart the process (by hitting Control+C and running node index again) and refresh the page it should look like this:
 
 ()
 
7.Integrating Socket.IO

Socket.IO is composed of two parts:
•	A server that integrates with the Node.JS HTTP Server: socket.io
•	A client library that loads on the browser side: socket.io-client

During development, socket.io serves the client automatically for us, as we’ll see, so for now we only have to install one module:
npm install --save socket.io
That will install the module and add the dependency to package.json. Now let’s edit index.js and the new index.js looks like:

()







[**NEXT**](https://github.com/sharathvontari/Socket.io/blob/master/Other%20Applications.md)     

[**BACK TO CONTENTS**](https://github.com/sharathvontari/Socket.io/blob/master/README.md)

