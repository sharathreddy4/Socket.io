##Sample Chat Application

- In this slide we are going to develop a simple chat application using node.js and socket.io.

Writing a chat application with other web applications such as PHP is difficult because it involves polling the server for changes, keeping track of timestamps, and it is also very slow. As asolution to this Sockets came up with better realtime chat systems which  providing a bi-directional communication channel between a client and a server.

- Setup:
1.The first thing is to setup a simple HTML webpage that serves out a form and a list of messages. We’re going to use the Node.JS web framework. So we should make sure that Node.JS is installed.

2.Let’s create a package.json manifest file that describes our project. 

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/images/images/image12.PNG)

3.Now, we will install express framework onto node.js.

npm install --save express@4.10.2

4.Now that express is installed we can create an index.js file that will setup our application.

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/images/images/image14.PNG)

This file helps us do the the following:

a.	Express initializes app to be a function handler that you can supply to an HTTP server.

b.	We define a route handler / that gets called when we hit our website home.

c.	We make the http server listen on port 8097.

5.Now if we run node index.js, we can see the following output on the terminal:

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/images/image1.png)
 
And if we type http://localhost:8097 in the browser, we should see it as below:

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/images/image2.png)

 
6.Creating HTML file

So far in index.js we’re calling res.send and pass it a HTML string. Our code would look very confusing if we further modified it by adding various features of our entire application’s HTML there. Instead, we’re going to create a index.html.

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/images/images/image16.PNG)

If you restart the process (by hitting Control+C and running node index again) and refresh the page it should look like this:
 
 ![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/images/image3.png)
 
7.Integrating Socket.IO

Socket.IO is composed of two parts:
•	A server that integrates with the Node.JS HTTP Server: socket.io
•	A client library that loads on the browser side: socket.io-client

During development, socket.io serves the client automatically for us, as we’ll see, so for now we only have to install one module:
npm install --save socket.io
That will install the module and add the dependency to package.json. So the new package.json looks like:

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/images/images/image13.PNG)

Now let’s edit index.js and the new index.js looks like:

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/images/images/image15.PNG)

8.Ultimately when we run node index.js and open a browser typing 'localhost:8097' we can see a msg is displayed on the nodejs command prompt which says 'user connected' as below:

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/images/image4.PNG)

9.Finally open two tabs in two different browsers or same browsers and try chatting. The output in the command prompt and the browsers would be as below:

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/images/image5.PNG)

![alt text](https://github.com/pkdevaraj/Presentations/blob/gh-pages/images/image6.png)





[**NEXT**](https://github.com/sharathvontari/Socket.io/blob/master/Other%20Applications.md)     

[**BACK TO CONTENTS**](https://github.com/sharathvontari/Socket.io/blob/master/README.md)

