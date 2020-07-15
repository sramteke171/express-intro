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

## Set up a basic Express server

Let's first create a directory for our app. We'll call it `fruit-app`.

```bash
mkdir fruit-app
cd fruit-app
```

Next we'll run `npm init` to initialize our app and create `package.json`.

```bash
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (fruit-app)
version: (1.0.0)
description:
entry point: (index.js) server.js
test command:
git repository:
keywords:
author:
license: (ISC)
About to write to C:\Users\ishaarora\Documents\cfg-seir-1\practice\fruit-app\package.json:

{
  "name": "fruit-app",
  "version": "1.0.0",
  "description": "",
  "main": "server.js",
  "dependencies": {
    "express": "^4.17.1"
  },
  "devDependencies": {},
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}


Is this OK? (yes) yes
```

After this if you run `ls` you'll see a new file `package.json`

Install Express by running `npm install express` in Terminal.

Now that the library has been installed (downloaded), we can use it in our code, by using the `require()` function.

But first we need to create a file called `server.js`

```bash
touch server.js
```

Open our app in vs code `code .`. 

Inside `server.js`, write the following

```javascript
const express = require('express');
```

- The `require()` function takes whatever code was written for the specified library and returns it
    - We'll typically store the return value of `require()` in a variable of the same name
        - Think of the variable as the library itself
- By reading [the documentation](https://www.npmjs.com/package/express), we can figure out how to use what is returned by  `require('express')`.


```js
const express = require('express'); //from documentation: express is function
const app = express();//app is an object

app.listen(3000, ()=>{
    console.log("I am listening");
});
    
```

1. Start the app by executing `node server.js` in the command line
1. Visit [http://localhost:3000/](http://localhost:3000/) in your browser.  You've successfully created a basic web server!  This will serve dynamic pages to web browsers.

## Set up a basic GET route

Now we'll create a basic GET route so that visitors to (clients of) our web-server can retrieve some information from it

```javascript
const express = require('express'); //from documentation: express is function
const app = express();//app is an object

app.get('/somedata', (req, res) => {
    res.send('here is your information');
});

app.listen(3000, () => {
    console.log("listening");
});
```

- The function passed as a second parameter to `app.get()` is executed each time a user (client) goes to `http://localhost:3000/somedata`
- The function (callback) takes two parameters
    - `req`
        - object containing information about the request made (browser, ip, query params, etc)
    - `res`
        - object containing methods for sending information back to the user (client)

Now let's open Postman app to call [http://localhost:3000/somedata](http://localhost:3000/somedata) to see what you get.

## Use nodemon to restart your sever when your code changes

An NPM package called `nodemon` allows us to run code just like `node`, but it will restart the application whenever code in the application's directory is changed.

1. Install it `npm install nodemon -g`
    - the `-g` tells npm to make the package available for use in the terminal in any directory (globally)
1. Now we can call `nodemon server.js`, and the server will restart whenever the app's code changes

## Closing Thoughts
- This afternoon we're going to learn more about the details of routes and resource serving in Express apps.
- Check your own understanding: Do you know the differences between Node's role and Express's role? What do each of them do?
- You'll be using this technology for the next several weeks!

## Create `.gitignore-global`
<!-- 
- In general, we don't want to store our package code in our repositories, because it increases the size of the repo unnecessarily
- We can install our packages like normal but keep track of what packages were installed in a `package.json` file.
    - Then when other users download our code
        1. They simply call `npm install`
        1. NPM will then look in the package.json file to see what packages need to be installed and install them without requiring the user to type `npm install some-package` for each package the app depends on (dependency)

1. In the terminal, type: `npm init`
1. Keep hitting enter, until the program finishes
    - you should now have a package.json file
1. Install a package with `npm install some-package --save`
    - The `--save` tells npm to keep a record inside `pacakge.json` that the application depends on the package installed

Let's test this out:

1. `rm -r node_modules`
1. `npm init`
1. `npm install express --save`
1. `rm -r node_modules`
    - simulates another developer downloading your code
1. `npm install`
1. Look inside the `node_modules` directory to see if `express` was installed
-->

In general, we can tell git to ignore `node_modules` directories so that they don't get added accidentally

1. In the Terminal, create a file called `.gitignore-global` in your Home directory. It will open the empty in VS Code.

   - `code ~/.gitignore-global`
   
1. In the file, copy and paste the code below. It's overkill, but it should ignore everything we'll use in class.

   ```bash
   # via https://github.com/github/gitignore unless otherwise noted
   # Currently includes:
   # - macOS
   # - Sublime Text
   # - VS Code
   # - Node (typically project-level gitignore, not global)

   # >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
   # macOS
   # >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
   # General
   .DS_Store
   .AppleDouble
   .LSOverride

   # Icon must end with two \r
   Icon


   # Thumbnails
   ._*

   # Files that might appear in the root of a volume
   .DocumentRevisions-V100
   .fseventsd
   .Spotlight-V100
   .TemporaryItems
   .Trashes
   .VolumeIcon.icns
   .com.apple.timemachine.donotpresent

   # Directories potentially created on remote AFP share
   .AppleDB
   .AppleDesktop
   Network Trash Folder
   Temporary Items
   .apdisk

   # >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
   # Sublime Text
   # >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
   # Cache files for Sublime Text
   *.tmlanguage.cache
   *.tmPreferences.cache
   *.stTheme.cache

   # Workspace files are user-specific
   *.sublime-workspace

   # Project files should be checked into the repository, unless a significant
   # proportion of contributors will probably not be using Sublime Text
   # *.sublime-project

   # SFTP configuration file
   sftp-config.json

   # Package control specific files
   Package Control.last-run
   Package Control.ca-list
   Package Control.ca-bundle
   Package Control.system-ca-bundle
   Package Control.cache/
   Package Control.ca-certs/
   Package Control.merged-ca-bundle
   Package Control.user-ca-bundle
   oscrypto-ca-bundle.crt
   bh_unicode_properties.cache

   # Sublime-github package stores a github token in this file
   # https://packagecontrol.io/packages/sublime-github
   GitHub.sublime-settings

   # >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
   # VS Code
   # >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
   .vscode/*
   !.vscode/settings.json
   !.vscode/tasks.json
   !.vscode/launch.json
   !.vscode/extensions.json

   # >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
   # Node
   # >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
   # Logs
   logs
   *.log
   npm-debug.log*
   yarn-debug.log*
   yarn-error.log*

   # Runtime data
   pids
   *.pid
   *.seed
   *.pid.lock

   # Directory for instrumented libs generated by jscoverage/JSCover
   lib-cov

   # Coverage directory used by tools like istanbul
   coverage

   # nyc test coverage
   .nyc_output

   # Grunt intermediate storage (https://gruntjs.com/creating-plugins#storing-task-files)
   .grunt

   # Bower dependency directory (https://bower.io/)
   bower_components

   # node-waf configuration
   .lock-wscript

   # Compiled binary addons (https://nodejs.org/api/addons.html)
   build/Release

   # Dependency directories
   node_modules/
   jspm_packages/

   # TypeScript v1 declaration files
   typings/

   # Optional npm cache directory
   .npm

   # Optional eslint cache
   .eslintcache

   # Optional REPL history
   .node_repl_history

   # Output of 'npm pack'
   *.tgz

   # Yarn Integrity file
   .yarn-integrity

   # dotenv environment variables file
   .env
   .env.test
   .env_local

   # parcel-bundler cache (https://parceljs.org/)
   .cache

   # next.js build output
   .next

   # nuxt.js build output
   .nuxt

   # vuepress build output
   .vuepress/dist

   # Serverless directories
   .serverless/

   # FuseBox cache
   .fusebox/

   # DynamoDB Local files
   .dynamodb/

   # Python
   __pycache__
   ```

1. Close down your Terminal and re-open. Now, going forward, git will ignore those files and folders when you git add.

<br>

## Update package.json

We can also edit `package.json` so that we don't need specify the script that we're going to run.  Do one of the following:

- After doing `npm init`
    - when it says `entry point: (index.js)`, specify which file you want to use (e.g. server.js)
- Edit package.json
    - where it says `"main": "index.js",` change the file name (e.g. server.js)

Now we can simply run `nodemon` without specifying the file name


## Additional Resources
1. <a href="http://expressjs.com/starter/installing.html" target="_blank">Starting an Express Project</a>
2. <a href="http://expressjs.com/starter/hello-world.html" target="_blank">Express Hello World</a>
3. <a href="http://expressjs.com/starter/static-files.html" target="_blank">Express Static Files</a>
4. <a href="http://expressjs.com/4x/api.html#res.render" target="_blank">Express res.render()</a>
