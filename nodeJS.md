# Node.js

[Node.js](https://nodejs.org/) is a JavaScript runtime for  server-side programming. It allows developers to create scalable backend functionality using JavaScript.

**Node.js uses asynchronous programming!**

Here is how Node.js handles a file request:

1. Sends the task to the computer's file system.
2. Ready to handle the next request.
3. When the file system has  opened and read the file, the server returns the content to the client.

Node.js eliminates the waiting, and simply continues with the next request. 

Node.js runs single-threaded, non-blocking, asynchronously programming, which  is very memory efficient.

### [Installing Node.js](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04)

```bash
sudo apt update
sudo apt install nodejs
node -v
Output
v10.19.0
```

**Warning:** the version of Node.js  included with Ubuntu 20.04, version 10.19, is now unsupported and  unmaintained. You should not use this version in production, and should  refer to one of the other sections in this tutorial to install a more  recent version of Node.

### Node Package Manager

[npm website](https://www.npmjs.com/)

```bash
sudo apt install npm
```

### Read Evaluation Print Loop

It represents a computer environment like a Windows console or  Unix/Linux shell where a command is entered and the system responds with an output in an interactive mode. Node.js or **Node** comes bundled with a REPL environment. It performs the following tasks −

- **Read** − Reads user's input, parses the input into JavaScript data-structure, and stores in memory.
- **Eval** − Takes and evaluates the data structure.
- **Print** − Prints the result.
- **Loop** − Loops the above command until the user presses **ctrl-c** twice.

### [Native Node Module](https://nodejs.org/en/docs/)

Native Node Modules are the **perfect tool for Node.js applications** that need to run performance critical code, access system level APIs, or include existing C/C++ libraries.

Example:

The `fs` module provides an API for interacting with the file system in a manner closely modeled around standard POSIX functions.

```javascript
const fs = require('fs');

// destination.txt will be created or overwritten by default.
fs.copyFileSync('source.txt', 'destination.txt');
console.log('source.txt was copied to destination.txt');

```

### External Node Module

First, initialize a node.js application by typing in **npm init** in the command prompt/terminal (make sure you are present in the current project folder). It will create a package.json file.

```bash
npm init
```

<u>Example</u>

[superheroes module](https://www.npmjs.com/package/superheroes)

```bash
npm install superheroes
```

```javascript
const superheroes = require('superheroes');
 
superheroes.all;
//=> ['3-D Man', 'A-Bomb', …]
 
superheroes.random();
//=> 'Spider-Ham'
```

### Summary

Node.js liberates JavaScript from the browser. We can run our code as a standalone application rather than something that can only be evaluated in a browser environment.

### References

https://www.tutorialspoint.com/nodejs/nodejs_repl_terminal.htm

https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04

https://docs.npmjs.com/

[Educative.io](https://www.educative.io/blog/what-is-nodejs?aid=5082902844932096&utm_source=google&utm_medium=cpc&utm_campaign=blog-dynamic&utm_term=&utm_campaign=Dynamic+-+Blog&utm_source=adwords&utm_medium=ppc&hsa_acc=5451446008&hsa_cam=8090938743&hsa_grp=82569843726&hsa_ad=396819070286&hsa_src=g&hsa_tgt=aud-477877425076:dsa-837938538428&hsa_kw=&hsa_mt=b&hsa_net=adwords&hsa_ver=3&gclid=Cj0KCQjws4aKBhDPARIsAIWH0JVV8HXMRJq3Da-yi7wYlq0dIRgFJudFCzNyghtYa9DL2dcv90vhBtEaAtYmEALw_wcB)



