# Exercise: Hello World in Express

Normally, JavaScript runs in the browser and it can only access your web page. Node.js is a platform for building **server-side** event-driven I/O application using JavaScript. It makes it possible to open or create new files, listen to network traffic, access databases and much more. Basically anything you can do with PHP or Ruby on Rails you can now do with JavaScript using Node.js.

Express.js on the other hand is a framework based on Node.js for building **web applications**. It gives you simply APIs to create your own little web server in a few lines of code.

## Scenario

Let's build our first web server using Node.js and Express.js and send a `Hello World` to anyone that sends a request to `/`.

While Node.js has a really great ES2015 support, we'll write our server in TypeScript.

## Tasks

1.  Create a new file `server.ts` in `/server`.
2.  To get started, import `express`. Since we are using TypeScript you can use the ES2015 import syntax, like so `import * as express from 'express'`.
3.  Create a new instance of express and assign it to a variable called `app`. When calling express, it will create a new instance and therefore an express _application_ which represents our server.
4.  Set up a constant for the port. The value is either the port specified in the environment variables or `5000`.
5.  Create a new `get` listener for `/`. The callback takes two parameters `req` and `res`, in exactly that order. Inside the callback use the response object to send `Hello World`.
6.  The last thing we have to do get express running, is to listen on a port. Use `app.listen()` to listens for connections on the specified host and port. This `listen()` function takes 3 parameters, a `port`, a `host` and a `callback`. For these parameters, use our port variable from before, skip the host as it is localhost anyways, and specify a callback. This callback is called when the server starts listening for requests.
7.  In order to test this, we first need to transpile the server to JavaScript. For that run `npm run webpack:server` or with yarn `yarn webpack:server`.
8.  When that's done, start the server with `node dist/server.js`.
9.  Open up your browser and go to `localhost:5000`. You should see `Hello World` being returned and rendered to the screen.

That's it! You implemented your own web server using Node.js and Express.js.

### Additional resources and help

* [Express API Reference 4.x](http://expressjs.com/en/4x/api.html)
