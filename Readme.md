# Why NodeJS?

NodeJs platorm can be run on various OS.
Huge no of third party pacakages are available to help us work better.  
It is Open Source.

## How To Run JavaScript using NodeJs?

There are 2 ways  
i)Node REPL(Read-Eval-Print-Loop)  
ii)Node CLI(Command Line Interface)

### Node REPL

The Node REPL is an interactive shell that processes Node Js Expressions.

### Node CLI

We can write JavaScript to a file and run using Node CLI.

```js
const add = (a, b) => {
  console.log(a + b);
};

add(1, 2);
add(3, 4);
```

# Exporting Modules

Each js file in node js is considered as a module.

## MODULE EXPORTS(Default Export)

The module.exports is a special object inculded in every JS file in the Node JS application.  
To import the module we use the require() function with the module name, we use ./ added to the name to locate the file.
We can only have single Default Export per module

```js
const add = (a, b) => {
  console.log(a + b);
};

module.exports = add;
```

## Named Export

On the modules.exports object we can set various properties. We can have multiple named exports per modules

```js
const add = (a, b) => {
  console.log(a + b);
};
const sub = (a, b) => {
  console.log(a - b);
};
module.exports.add = add;
module.exports.sub = sub;
```

We cannot export boolean, number, string, null, undefined, objects, and arrays while defining.

# Diving Deep Into NodeJS
NodeJS helps us to run JS outside the web browser. 
In general Node js has V8 engine and some extra features.
Javascript engines on the web are used to run the Javascript. One such famous engine is the V8 engine. 
A fact is that JS runs using c++ code i.e the javascript engines like V8 for eg are made using C++ code. SO, we can say that the node js code runs using C++ code of teh V8 engine.

These engines are built on constraints applied by the ECMASCRIPT. This is a foundation that defines rules that tell what are the general function a JS engine should contain.
These engines convert the JS code into low level codes(i.e machine code, assembly code).

NodeJS is JS runtime environment. 

A global object is an object that is accessible everywhere in your code. It provides variables and functions that are available by default in any JavaScript environment. 
In Node this global object is called "global". This global can be classified as a sueprpower in NodeJS

The require method only executes the code but we cannot access the variable or methods in the file. For accessing variable or methods we use "module.exports"

eg:- 
```js 
  //exporting single item
  module.exports = calculate_sum;

  //exporting multiple items
  module.exports = {
    x: x,
    cs: calculate_sum,
  }
``` 

JS executes these require statements synchronusly.  

We cannot access the variable of the file in require method because JS wraps the code into a function and therefore the cannot be accesed when we use require. 
This function is a special type of function called as IIFE(Immediately Invoked Function Expression). IIFE is an anonymous function that is immediately Invoked.

```js 
(function (){

  //All the code of the module runs here

})();

```
In IIFE module.exports = {} is a parameter so we can access the functions/methods of different files by using module.exports.

eg:-
```js
(function (module){

    var a = 10;
    var b = 20;
    module.exports = {
      a:a,
      b:b};
})(module);
```
# libuv

JS does not have features like connecting to DB and requestion data from a website and other resources also JS does not have timer. 
These are the features that are related to communciation between the Operating System(OS).  
This is where NodeJS comes into pictures. It helps JS communciating with the OS by using a library caled libuv. 

When V8 engine encounters an API it offloads it to the libuv and goes to the next part. 
NodeJS is async but v8 engine is sync. The async operations are offloaded to the libuv which completes the tasks and returns the 
result and the call back function to the v8 engine for execution. This is the reason it is called as async I/O or non blocking I/O. 

```js 
const fs = require('fs')
const https = require('https')

console.log("Hello World!")

var a = 10
var b = 20

setTimeout(() => {
    console.log("Set Timeout executed")
},5000)

https.get('https://dummyjson.com/products/1',(res)=>{
    console.log('Data fetched')
})

fs.readFile('./hello.txt','utf-8',(err,data)=>{
    console.log("File:",data)
})
/*
Output:-
Hello World!
File: hello world! this is karthik
Data fetched
Set Timeout executed
*/
```
This is the best example for how the async operation work in JS. 

Synchronus functions should not be used as they hold up the main thread.

# V8 Engine 
A) Parsing
    1) Lexical Analysis(Tokenization):- Code given is broken down into tokens.
    2) Syntax Analysis: An abstract syntax tree is generated for the token. 
B) Interpreter(Ignition Interpreter):- Converts code to byte code
C) Compiler (Turbo Fan Compiler):- Optimized code and converts into machine level code 

# Event Loop

It move the callbacks to callstack for execution if and only if the callstack is empty.

There are 4 phases in Eventloop:
1) Timer:- This is the first phase in event loop. Here all the setTimeout() and setIntervals() are prioritized and 
are moved to the call stack for execution. 
2) Poll:- After the timer phase comes the Poll phase all the callbacks associated with I/O callbacks(i.e data, fs, crypto, http.get, etc) are moved to the call stack 
3) Check:- In the check phase all the callbacks associated to setImmediate are executed.  
4) Close:- Callbacks associated with socket.close are executed.

Before every phase eventloop will follow an inside cycle. This inner cycle will be executed before every outer phase. 


## Monolith

A monolithic architecture is a traditional approach to designing software where an entire application is built as a single, indivisible unit.  
This means that any changes or updates to the application require modifying and redeploying the entire project.  
This type of architecture generally suits small scale projects.  

## Microservices

A microservices architecture is an application is built as a collection of small, independent services, each representing a specific business capability. 
These services are loosely coupled and communicate with each other over a network, often using lightweight protocols like HTTP or messaging queues.

'^' this symbol is called caret is used as a version range indicator for dependencies in Node.js projects. It specifies that the package can be updated to any minor or patch version that is compatible with the specified major version.
