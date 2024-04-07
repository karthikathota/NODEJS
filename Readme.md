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
