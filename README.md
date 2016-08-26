<!--
Creator: Cory Fauver
Market: SF
-->

![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png)

# Node.js and Express

### Why is this important?
<!-- framing the "why" in big-picture/real world examples -->
*This workshop is important because:*

These are the first tools we'll use to write server-side code. In order to be a **full-stack** web developer, you'll need to have a grasp on writing code on the backend. Node and Express are the industry standard technologies for writing server-side JavaScript. If you find yourself working in an environment that using a full JS stack, you will be using Node.js and Express. Node is a lightweight and efficient runtime for building JavaScript servers. Express is a very popular and trending framework with a bevy of modules you can add to it.

### What are the objectives?
<!-- specific/measurable goal for students to achieve -->
*After this workshop, developers will be able to:*

- draw a diagram of the request response cycle with Node.js and Express included and labeled.
- describe the roles that Node.js and Express play in building a server.
- use `npm` to initialize a node project and write a local web server to serve JSON and static assets with Express.


### Where should we be now?
<!-- call out the skills that are prerequisites -->
*Before this workshop, developers should already be able to:*

- draw a figure of the request-response cycle with the details filled in on the front end (user, event listeners, AJAX, success callbacks, and HTTP verbs).
- make an AJAX request to a third party API and explore the JSON data it returns.



### Motivation (Why?)

Express is a cutting-edge, unopinionated, server-side JavaScript framework that runs on a Node.js server. It is a very, very popular and trending framework with a bevy of modules you can add to it.

### What is Node?
- Node.js is a webserver that operates on the V8 Google Chrome JavaScript runtime, allowing you to write server-side code in JavaScript.
- Node.js provides the ability to handle requests and issue responses.
- It is fast.
- It is fast largely because it is asynchronous, meaning code can run in parallel without "blocking" the call stack (the list of other concurrent commands).

### NPM and NPM Init
- NPM stands for Node Package Manager, and is a tool that allows us to easily download community-built Node packages.
- Initialize new Node project with NPM: `npm init`.
- Install NPM packages: `npm install --save express`.
- NPM works with package.json, which is a list of project information and dependencies that can be installed on other computers and servers.

### What is Node Good For?
- Node really shines when it comes to heavy input-output type operations.
- Realtime services like chat applications or conferencing platforms benefit from using Node.
- APIs are also input/output heavy, and they also tend to work with JavaScript out of the box (think JSON). What better platform than Node?

### Express JS
- Express is a framework built on top of Node.js that makes development of web servers more intuitive and quicker.
- Express allows us to easily set up routes that will trigger actions such as rendering pages or returning JSON.

### Hello World in Express

```javascript
var express = require('express');
var app = express();

app.get('/', function (req, res) {
  res.send('Hello World!');
})

var server = app.listen(3000);
```

### Request Response Cycle

Remember that the interwebs is many clients querying many servers. We've done a lot with clients and APIs, and now we want to write the server side code that handles the request and then responds with some data.

![request](http://i.imgur.com/YXgj8.png)


### Express file tree

```
├── server.js  // your server code
├── package.json    // lists dependencies; changed by npm install --save somePackage
├── public  // i.e. client-side
│   ├── images  // images to serve to client
│   ├── scripts
│       └── app.js   // client-side javascript file
│   └── styles
│       └── style.css
├── vendor // optional 2nd public dir for jQuery & bootstrap if we choose not to use CDNs
├── views  // html files that we'll serve
│   └── index.html
└── node_modules  // don't edit files in here!
    ├── express // etc
```

> We should also add `node_modules` to a `.gitignore` file so it is not checked into git.  Future developers can just run `npm install` to get the packages listed in `package.json`

**In Express**

Let's look at a basic `get` method in an express app.

```js
// server.js
  var taquerias = [
    { name: "La Taqueria" },
    { name: "El Farolito" },
    { name: "Taqueria Cancun" }
  ]
```

```js
  app.get('/api/taquerias', function (req, res) {
    res.json(taquerias);
  });
```

Note that the `app` object has a method called `.get()` which takes two arguments: a url and a callback function. The callback takes two arguments: `req` and `res`. These stand for "Request" and "Response" from the request response cycle. We'll be console logging these objects in the exercises.

### Game Plan

Today's <a href="https://github.com/SF-WDI-LABS/express-intro" target="_blank">exercises</a> are set up a bit like a tutorial to walk you through:

  * creating a new project with Node and Express
  * creating routes for clients to make requests to your server
  * storing data on the server
  * responding to GET requests with simple strings (`res.send`), or JSON data (`res.json`)
  * serving static files (images, css...)


### Docs, Resources, Further Reading

1. <a href="http://expressjs.com/starter/installing.html" target="_blank">Starting an Express Project</a>
2. <a href="http://expressjs.com/starter/hello-world.html" target="_blank">Express Hello World</a>
3. <a href="http://expressjs.com/starter/static-files.html" target="_blank">Express Static Files</a>
4. <a href="http://expressjs.com/4x/api.html#res.render" target="_blank">Express res.render()</a>

###Check for Understanding

<details>
  <summary>Thought provoking question</summary>
  <p>Mind-blowing explanation</p>
</details>

## Independent Practice
Refine the skills covered in this workshop with this [lab](#)

## Closing Thoughts
- review objectives & hierarchy of importance
- look ahead & link to future workshops
- clarify expectations and what developers should know by now
- reiterate “the why” with a perspective of your intentions
- create an active recall
- Check for understanding

## Additional Resources
- [External Resource](#)
