---
title: 'Node Js'
date: 2024-12-19
draft:  false   
featured: false  
description: "Node Js"
thumbnail: "/posts/markdown/images/"
featureImage: "/posts/markdown/images/" 
shareImage: "/posts/markdown/images/"
author: "Angel Vyas"
math: true
enableEmoji: true
tags:
    - NodeJs
categories:     
    - General
---

### Create a custom server using http module and explore the other modules of Node JS like OS, path, event.

### File 1: os.js
```java
const os=require('os');
console.log('Data retrieved by Using OS Module in Node Js\n');
console.log('Hostname:'+os.hostname()+'\n');
console.log('Architecture:'+os.arch()+'\n');
console.log('OS Platform:'+os.platform()+'\n');
console.log('OS Type'+os.type()+'\n');
var freeMemory=os.freemem();
console.log('Free RAM:'+Math.round(freeMemory/1024/1024/1024)+'GB\n');
var totalMemory=os.totalmem();
console.log('Total RAM:'+Math.round(totalMemory/1024/1024/1024)+'GB\n');
```

### File 2: path.js
```java
const path = require('path');
console.log('File Name: \n'+__filename+'\n\n');
console.log('Directory Name: \n'+__dirname+'\n\n');

console.log('Base Name of File Name: \n'+path.basename(__filename)+'\n\n');
console.log('Base Name of Directory Name:\n'+path.basename(__dirname)+'\n\n');
var data = path.parse(__filename);
console.log('Parser Data: \n');
console.log(data);
console.log('\n\n');
console.log('isAbsolute for __filename: '+path.isAbsolute(__filename)+'\n');
console.log('isAbsolute for given relative file : '+path.isAbsolute('./os.js')+'\n');
console.log(path.join("MGIT","ET","CSM and CSD"));
console.log(path.join("/MGIT","ET","CSM and CSD"));
console.log(path.join("/MGIT","//ET","CSM and CSD"));
console.log(path.join("/MGIT","//ET","../CSM and CSD"));
console.log(path.join(__dirname,"CSM and CSD"));
```

### File 3: event.js
```java
var fs = require('fs');
var rs = fs.createReadStream('./myfile.txt');
rs.on('open', function () {
console.log('The file is open');
});
var events = require('events');
var eventEmitter = new events.EventEmitter();
//Create an event handler:
var myEventHandler = function () {
console.log('Welcome to Node Js Lab...!');
}
//Assign the event handler to an event:
eventEmitter.on('welcome', myEventHandler);
//Fire the 'welcome' event:
eventEmitter.emit('welcome');
```
### for output:
install Nodejs on your system.
create myfile.txt
for execution on terminal: node filename.js

