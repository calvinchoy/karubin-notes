---
title: ES6 Fundamentals
tags:
  - javascript
  - es6
categories:
  - - javascript
date: 2018-11-06 22:27:54
---


An overview of some popular features in ES6 (ECMAScript6) that are often used. For a complete overview of the specifications you can visit [ES6 Standards](http://www.ecma-international.org/ecma-262/6.0/) and [ES6 Features](http://es6-features.org/).

<!-- more -->

## Arrow functions
ES6 introduces a new syntax for shorter function declaration. This new notation does __not__ shadow `this` and is useful for short callback functions.

Inside the arrow function, the `this` binding is not dynamic but is instead lexical. The `=>` notation replaces the `self = this` 'hack' used for example to access the `this` binding of the parent context.

```javascript
//Expression single parameter notation
par1 => par1 + 1

//Expression multiple parameters notation
(par1, par2) => par1 * par2

//Statement bodies
par1 => {
  //body content . . .
}

```
## Variables and scoping
* `let` is the new `var` for declaring variables and is scoped without the hoisting.
* Use `const` to declare constants.

## Classes
Syntactical sugar for creating OOP classes and functionalities. Instead of using the prototype-based inheritance creating classes is now more intuitive and friendly. ES6 classes supports class extension, constructor, instances and super calls.

```javascript
//Base class
class Shape {
    constructor (id, x, y) {
        this.id = id
        this.move(x, y)
    }
    move (x, y) {
        this.x = x
        this.y = y
    }
}

//class extension
class Rectangle extends Shape {
    constructor (id, x, y, width, height) {
        //call parent constructor using super
        super(id, x, y)
        this.width  = width
        this.height = height
    }
}
class Circle extends Shape {
    constructor (id, x, y, radius) {
        //call parent constructor using super
        super(id, x, y)
        this.radius = radius
    }
}
```

## Enhanced object literals
Bringing classes and object literals closer together. Some main enhancements:
* Shorthand notation when name and value use same name
* Supporting methods
* Property names by expression

```javascript
var litObject = {
    // Shorthand for foo: foo’
    foo,
    // Method properties
    someMethod() {

    },
    // names by expression
    ["foo" + bar()]: 10
};
```

## Template strings
ES6 now supports string interpolation

```javascript
//String interpolation using `` notation
let firstname = "John";
let lastname = "Doe";

let fullname = `The fullname is ${firstname} ${lastname} and age is ${20+10}`;
```
## Destructering assignment
ES6 introduces a new syntactic feature called destructuring. I can be used for declaration and assignment of variables. Two syntax are introduced: array destructuring and object destructuring.

<!-- more -->

### Array declaration destructuring

Destructuring uses the left hand side of the `=` assignment as a pattern for decomposing the right side array value output. Example

__Before__

```javascript
function foo(){
    return [1,2,3];
}

//assigning array output to individual variable
var temp = foo();

var a = temp[0];
var b = temp[1];
var c = temp[2];

```

__Using destructuring:__

```javascript
var [a, b, c] = foo():
```

Destructuring uses the left hand side of the `=` assignment as a pattern for decomposing the right side array value output.

### Object declaration destructuring

Similar with array destructuring we can define a pattern for assigning object property values. Example:

```javascript
function bar(){
    return {
        x:6.
        y:7,
        z:8
    }
}

var {x:x, y:y, z:z} = bar();
```

If the property name is the same, we can actually use a shorter syntax. This can be done by leaving out the `x:` (left) part of the declaration:

```javascript
var {x, y, x} = bar();
```

The longer syntax is usefull when you want to assign a different name:

```javascript
var {x:bam, y:baz, z:bap} = bar();
console.log(bam, baz, bap) //6, 7, 8
```

Notice how the `{name:value}` synax is flipped into `{target-name: alias}` with will result in `{ alias: target-value}`


Also, assigning using destructuring you don't need to assign al available values:

```javascript
var [,b] = foo();
var {x, z} = bar();
```

## Default parameter values
There is now support for default parameter values

```javascript
function f (x, y = 7, z = 42) {
    return x + y + z
}
f(1) === 50
```

## Rest parameter
Replacement for variable arguments. Aggregates arguments into a single argument using the triple dot `...` notation

```javascript
function f (x, y, ...restParameter) {
    return (x + y) * restParameter.length
}

//hello, true and 7 are collected in restParameter as an array
f(1, 2, "hello", true, 7) === 9
```

## Spread operator
Spreading of elements of an iterable collection (like an array or even a string) into both literal elements and individual function parameters.

```javascript
//Function
let coordinates = [1,2,3];

function point3D(x, y, z){
  //implementation . . .
}

point3D(...coordinates);

//String
let str = "foo"
let barChars = [ ...str ] // [ "f", "o", "o" ]
```

## Modules
Exporting/importing specific parts from modules

### Export

```javascript
//export function and variable for SomeFile.js
export function test(){...}
export let par1 = 1

//default export
export default function (par){
  //implementation...
}

//export from another module using wildcard * (like extending)
export * from "AnotherModule"
```

### Import
```javascript
//import everything from SomeFile.js using wildcard *
import * as somefile from "SomeFile"

//import selectively
import {test} from "SomeFile"
```

## Promises
Promises are a first class representation of a value that may be made available in the future. It solves the callback hell with aysynchronous programming.

```javascript
//function implementation returning a promise
function someAsyncOperation(param){
  //implementation details...

  return new Promise((resolve, reject) => {
        //implementation details...
    })
}

someAsyncOperation(someParams)
.then(function(result){
    // Do something with the result
})
.catch(function(error){
    // Handle error
});
```

## Resources
* [ECMAScript6 Specifications](https://www.ecma-international.org/ecma-262/6.0/)
* [ES6 Features](http://es6-features.org/#Constants)
* [ES Quick Overview](https://github.com/lukehoban/es6features#readme)
