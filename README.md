<!--
Creator: Cory Fauver & Justin Castilla
Market: SF
-->

![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png)

# Node.js and Express

### Why is this important?
<!-- framing the "why" in big-picture/real world examples -->
*This workshop is important because:*

These are the first tools we'll use to write server-side code. In order to be a **full-stack** web developer, you'll need to have a grasp on writing code on the backend. Node and Express are the industry standard technologies for writing server-side JavaScript. If you find yourself working in an environment that uses a full JS stack, you will be using Node.js and Express. Node is a lightweight and efficient runtime for building JavaScript servers. Express is a very popular and trending framework with a bevy of modules you can add to it.

### What are the objectives?
<!-- specific/measurable goal for students to achieve -->
*After this workshop, developers will be able to:*

- describe the roles that Node.js and Express play in building a server.
- draw a diagram of the request response cycle with Node.js and Express included and labeled.
- use `npm` to initialize a node project and write a local web server to serve JSON and static assets with Express.


### Where should we be now?
<!-- call out the skills that are prerequisites -->
*Before this workshop, developers should already be able to:*

- draw a figure of the request-response cycle with the details filled in on the front end (user, event listeners, AJAX, success callbacks, and HTTP verbs).
- make an AJAX request to a third party API and explore the JSON data it returns.

## What is a server?

<details>
  <summary>Take 5 minutes to search the web to pull together a working definition of what a "server" is and what it does.</summary>
  <h5>Meta question: how did you go about searching? </h5>
</details>

## What does it mean to program a server?

We need to write the code that handles requests and figures out how to respond. It might need to format data into JSON, it might need to talk to a database to request a specific resource, and it might need to check if a user is authorized to see the resource they have requested.

To write server side code, is to lay out all of the possible requests that might come in and give instructions for how to handle each type of request.

![request](https://i.imgur.com/YXgj8.png)


![image](https://cloud.githubusercontent.com/assets/6520345/18041555/0345ba10-6d6f-11e6-9a6f-c008aac1935a.png)

### What is Node?

![image](https://cloud.githubusercontent.com/assets/6520345/18023104/d38c2168-6ba9-11e6-997c-24b3a2652991.png)

![image](https://cloud.githubusercontent.com/assets/6520345/18023096/c368ce26-6ba9-11e6-805a-4562a8853721.png)

V8, the JavaScript engine that runs Chrome, is a piece of code written in C++. It creates a processor to take in JS code and translate it to make actionable assembly code/machine code so that the CPU can “do” what you have asked it to in JavaScript. Node is a program that has all of the V8 code and more. It extends V8; V8 is embedded in NodeJS, and Node adds more functionality and syntax that V8 wouldn’t be able to understand. This syntax allows you to write server-side code. (V8 is created to meet the EcmaScript 6 - the standard that defines JavaScript).

- Node.js provides the ability to handle requests and issue responses.
- It is fast.
- It is fast largely because it is asynchronous, meaning code can run in parallel without "blocking" the call stack (the list of other concurrent commands).
- Node really shines when it comes to heavy input-output type operations.
- Realtime services like chat applications or conferencing platforms benefit from using Node.
- APIs are also input/output heavy, and they also tend to work with JavaScript out of the box (think JSON). What better platform than Node?
- Node is designed to accommodate [the module pattern](https://addyosmani.com/resources/essentialjsdesignpatterns/book/#modulepatternjavascript), which means that it allows developers to write useful functionality and then share it with other developers. It is easy to pull in useful modules into your project (like express). This keeps functionality separate and helps projects feel organized.

### NPM and NPM Init
- Node Package Manager, usually called NPM, is a tool that allows us to easily download community-built Node packages.
  * For example, instead of using a CDN to download bootstrap and make sure your version is up-to-date, you can install it with NPM, which will help you manage the downloads and versions.
- Initialize new Node project with NPM: `npm init`. This will simply create one file, `package.json`.
- NPM works with `package.json`, a file in your project, which is a list of project information. NPM makes sure that packages do not get uploaded or tracked in git (imagine how much unnecessary code you could be pushing and pulling each time). To make sure all collaborators are still on the same page, any package listed in `package.json` can easily be downloaded with one command, `npm install`, when somebody clones your project.
- To install NPM packages *and* save them to `package.json`, use the `--save specification`: `npm install --save express` or `npm install --save bootstrap`.



### Express JS
Express is a cutting-edge, unopinionated, server-side JavaScript framework that runs on a Node.js server. It is a popular framework with a bevy of modules you can add to it. Node is the platform and Express provides the specific functionality. If you were building a house rather than a server, Node would be the foundation and utilities, express would be the building material that comprises the above ground building.

![image](https://cloud.githubusercontent.com/assets/6520345/18060592/f5954682-6dd3-11e6-99ba-5dc0b42a4ff8.png)




- Express is a framework built on top of Node.js that makes development of web servers more intuitive and quicker.
- Express allows us to easily set up routes that will trigger actions such as rendering pages or returning JSON.

Much like jQuery does for JavaScript, Express provides easy, intuitive syntax and a lot of built in functionality.

### Hello World in Express

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => res.send('Hello World!'))

const server = app.listen(3000);
```




### Express file tree

With frontend and backend code to organize, we should make sure to keep our files in a logical order.

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
  let taquerias = [
    { name: "La Taqueria" },
    { name: "El Farolito" },
    { name: "Taqueria Cancun" }
  ]
```

```js
  app.get('/api/taquerias', (req, res) => res.json(taquerias) );
```

Note that the `app` object has a method called `.get()` which takes two arguments: a url and a callback function. The callback takes two arguments: `req` and `res`. These stand for "Request" and "Response" from the request response cycle. We'll be console logging these objects in the exercises.

### Game Plan

Today's [exercises](https://git.generalassemb.ly/sf-wdi-45/express-intro-lab) are set up a bit like a tutorial to walk you through:

  * creating a new project with Node and Express
  * creating routes for clients to make requests to your server
  * storing data on the server
  * responding to GET requests with simple strings (`res.send`), or JSON data (`res.json`)
  * serving static files (images, css...)



## Closing Thoughts
- This afternoon we're going to learn more about the details of routes and resource serving in Express apps.
- Check your own understanding: Do you know the differences between Node's role and Express's role? What do each of them do?
- You'll be using this technology for the next several weeks!

## Additional Resources
1. <a href="http://expressjs.com/starter/installing.html" target="_blank">Starting an Express Project</a>
2. <a href="http://expressjs.com/starter/hello-world.html" target="_blank">Express Hello World</a>
3. <a href="http://expressjs.com/starter/static-files.html" target="_blank">Express Static Files</a>
4. <a href="http://expressjs.com/4x/api.html#res.render" target="_blank">Express res.render()</a>
