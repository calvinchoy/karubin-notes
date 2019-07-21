---
title: OOP JavaScript Summary
tags:
  - oop
  - javascript
  - summary
categories:
  - [javascript]
  - [summaries]
date: 2018-11-02 13:45:34
---


In this article I we will go through some basics of Object - Oriented programming with JavaScript. A good refresher before getting into ES6 (ECMAScript2015).

<!-- more -->

# Primitive types
Primitive types represent simple pieces of data that are stored as is. A variable holding a primitive directly contains the primitive value. There are five primitve types in Javascript:

* Boolean - `true` or `false`
* Number - integer or floating-point
* String - Character or sequence of character
* Null - initialized with `null` value, unset but initialized variable
* Undefined - variable tat is not initialized


# Reference types
Reference types represent objects in javascript. Reference values are instances of reference types and are synonymous with objects.

Reference types do not store the object directly into the variable to which it is assigned, so the object variable in this example doesn’t actually contain the object instance. Instead, it holds a pointer (or reference) to the location in memory where the object exists.

This is the primary difference between objects and primitive values, as the primitive is stored directly in the variable.

## Built in reference types

* Array
* Date
* Error
* Function
* Object
* RegExp

To identify reference types use the `instanceof` operator.

# Comparing without coercion `(== vs ===)`
Double equals convert the type before comparing, where triple equals doesn't consider variables to be the same if the type is not equal.

# Objects
An object is an unordered list of properties consisting of a name (always a string) and a value. When the value is a function we call it a method.

There are a couple of ways to instantiate objects:

1. Use the `new` operator with a constructor (any function can be a constructor)

```javascript
var object = new Object();
```

2. Use the literal notation

```javascript
var object = {prop1:value,prop2:value}
```

## Detecting object properties ##
Use the `in` operator to detect existance of properties in the object. The `in` operator checks for both own properties and prototype properties. If you want to check for own properties only use the `hasOwnProperty()` method.

## Property attributes ##
There are two common types of properties: data and accesor. Two property attributes are shared between data and accesor properties:

* `Enumerable`: which determines whether you can iterated over the property
* `Configurable`:  which determines whether the property can be changed (i.e. delete)

By default these common properties are set to `true`. The properties can be set using the `Object.defineProperty(object, proplabel, config)` method. For example:

```javascript
var someObject = {
    label: "value""
}

Object.defineProperty(someObject, "value", {
    enumerable: false,
    configurable: false
});
```

### Data properties

* `value`: holds the property value
* `writable`: a boolean value indicating whether the property can be written to. By default all properties are writable.

Example:

```javascript
var person1 = {};

Object.defineProperty(person1, "name", {
    value: "Nicholas",
    enumerable: true,
    configurable: true,
    writable: true
});
```

### Accessor properties
Because there is no value stored for accessor properties, there is no need for `value` or `writable`. Instead, accessors have `get` and `set`, which contain the getter and setter functions, respectively.

Example:
```javascript
var person1 = {
    //_property act as private property
        _name: "Nicholas"
};

//create new property and setting common attributes
//and accesor attributes
Object.defineProperty(person1, "name", {
    get: function() {
        console.log("Reading name");
        return this._name;
    },

    set: function(value) {
        console.log("Setting name to %s", value);
        this._name = value;
    },

    enumerable: true,
    configurable: true
});
```

### Defining multiple properties (data and accessor)
It’s also possible to define multiple properties on an object simultaneously if you use `Object.defineProperties()` instead of `Object.defineProperty()`. This method accepts two arguments: the object to work on and an object containing all of the property information. The keys of that second argument are property names, and the values are descriptor objects defining the attributes for those properties.

Example:
```javascript
var someObject = {};

Object.defineProperties(someObject,{

    //define a data property
    _name: {
        value: "Calvin",
        enumerable: true,
        configurable: true,
        writable: true
    },

    //define accessor property
    name: {
        get: function(){
            return this._name;
        },
        set: function(value){
            this._name = value;
        }
});

```
## Preventing Object modification
Object, just like properties, have internal attributes that govern their behavior. There are three different ways to prevent object modification:

### 1. Preventing extensions
By default all objects are extensible, meaning that properties can be added to the object at any time. To create nonextensible objects the `Object.preventExtensions()` method can be used.This method accept a single argument, which is the object you want to make nonextensible.

### 2. Sealing objects
A sealed object is nonextensible, and all of its properties are nonconfigurable. That means you can not add and remove properties. You can only read and write to properties. To seal an object, use the `Object.seal()` method.

### 3. Freezing objects
Finally, we can create a nonextensible object by freezing it. A frozen object is a sealed object where data properties are also read-only. To freeze an object use the `Object.freeze()` method.

# Functions
There are two literal forms of functions, function declaration and function expression. Function declaration begins with the `function` keyword and includes the name of the function:

```javascript
function functionname(param1, param2){
    //code here...
}
```

Function expression on the other hand doesn't require a name after function and uses variable declaration notation:

```javascript
var functionname = function(param1, param2){
    //code here...
}
```
__Hoisting__

Function declarations are _hoisted_ to the top of the context. That means you can actually define a function after it is used in code without generating an error.

# Constructors and prototypes

## Constructors
A constructor is a function that is used with `new` to create your own objects besides the built-in javascript constructors. The first letter of a constructor is capitalized.

Constructors allow you to innitialize an isntance of a type in a consistent way. Use the `Object.defineProperty()` inside a constructor to help initializing the instance.

For example:
```javascript
function Person(name) {

    Object.defineProperty(this,
        "name", {
            get: function() {
                return name;
            },
            set: function(newName) {
                name = newName;
            },
            enumerable: true,
            configurable: true
        });

    this.sayName = function() {
        console.log(this.name);
    };
}
```
## Prototypes
Almost every function has a `prototype` property that is used during creation of new instances. The properties of the prototype can be accessed by all instances. By default all object share the properties of `Object.prototype`.

When a property is read on an object, javascript does the following:

1.  The engine looks for an own property with that name
2.  If an own property is not found, it will continue to look for the property in the prototype
3.  Finally, if no property is found with that name, `undefined` is returned.

Remember that `delete` property only works on own properties, you cannot delet a prototype property using `delete`.

### Using prototypes with Constructors
The prototype object is ideal for defining methods that are shared between all instances of a custom object. This could reduce duplicate code in instances. Use `this` to refer the current instance.

Example:
```javascript
//create constructor
function Person(name){
    this.name = name;
}

//define prototype method for Person constructor
Person.prototype.sayName = function(){
    console.log(this.name);
};
```

Changes to the `prototype` are immediately available on any instance referencing it.

Instead of definining the prototype properties one by one you can use the object literal. However, make sure you set the proper `constructor` value. By default the function name is set as constructor. The constructor is set to Object by default.

# Inheritance
In javascript it is possible to let inheritance occur between objects with no classlike structure defining the relationship. This is called _prototype chaining, or prototypal inheritance_. By default, the Object.prototype is always inherited with the following five methods:

* `hasOwnProperty()`. Determines whether an own property with given name exists.
* `propertyIsEnumberable()`. Determines whether an own property is enumerable.
* `isPrototypeOf()`. Determines whether the object is the prototype of another.
* `valueOf()`. Returns the value representation of the object.
* `toString()`. Returns a string representation of the object.

Do not ever modify the `Object.prototype`.This will affect __all__ objects.

## Object Inheritance
 By default object literals have `Object.prototype`set as their prototype implicitly. You can override this behaviour by explicitly specify the prototype with the `Object.create()` method.

Example:
```javascript
var person1 = {
    name: "Nicholas",
    sayName: function() {
        console.log(this.name);
    }
};

var person2 = Object.create(person1, {
    name: {
        configurable: true,
        enumerable: true,
        value: "Greg",
        writable: true
    }
});
```

## Constructor Inheritance
When a constructor is created, it becomes a subtype of `Object.prototype`. The constructor value is automatically set to the name of your constructor (function). As with Object inheritance discussed previously, this happens by using the `Object.create()` method.

## Constructor stealing and supertype methods
To call (steal) the supertype constructor from another constructor use the `call()` or `apply()` method.

Example:

```javascript
function ParentConstructor(par1, par2){
    //some subconstructor code
}

function ChildConstructor(par){
    //steal another constructor
    ParentConstructor.call(this, par, par)
}
```
In the same manner we can call supertypes methods in subconstructor methods.

Example:
```javascript
function someChildMethod(){
    //make call to another constructor
    ParentConstructor.prototype.someParentMethod.call(this);
}
```

<sub>This is an excerpt from the book: The Principles of Object - Oriented JavaScript</sub>
