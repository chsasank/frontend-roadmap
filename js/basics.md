# Basics of JS

Good cheat sheet: https://learnxinyminutes.com/docs/javascript/

## Comments and stuff

```js
// Single-line comments
/* These are
   multi line comments */

// Statements can be terminated by ; or not
console.log("hello world");
console.log("hey");
// btw, console.log is print of the js world
```

## Variables

```js
// this is global variable. avoid.
x = 3;
// what you normally wanna do.
var y = 3;
// you can declare undefined variable
var z;
// there's also null variables
var w = null;
// false, null, undefined, 0 and "" are falsy, everything else is truthy.
if (!w) {
  console.log("nope");
}
```

## Strings, arrays and objects

### Strings

```js
"This is a string".charAt(0);
// = 'T'
"Hello world".substring(0, 5);
// = 'Hello'
"Hello".length;
// = 5
```

### Arrays, aka list

```js
var myArray = ["Hello", 45, true];
// index starts at 0 like any sane language. Looking at you, lua.
myArray[0];
// = 'Hello'

// you can push and stuff
myArray.push("World");
// = 4

myArray.pop();
// = 'World'

// size of array
myArray.length;
// = 3

// Use join to do delimited string joins. very handy.
myArray.join(",");
// = 'Hello,45,true'
```

### Objects, aka dict or map

```js
// keys need not be in quotes for sane keys
var myObj = { myKey: "myValue", "my other key": 4 };
// index either with dot or subscript syntax
myObj.myKey;
// = 'myValue'
myObj["myKey"];
// = 'myValue'
myObj.anotherKey = "new world";
// = 'new world'
myObj;
// = { myKey: 'myValue', 'my other key': 4, anotherKey: 'new world' }
```

## Control flow

### if/else

```js
var count = 1;
if (count == 3) {
  console.log("hello");
} else if (count == 4) {
  console.log("hey");
} else {
  console.log("hi");
}

// use && and ||
if (count > 0 && count < 2) {
  console.log("0 < x < 2");
}

if (count < 0 || count > 2) {
  console.log("x not in (0,2)");
}
```

### while loop

```js
var myArray = ["Hello", 45, true];
var idx = 0;
while (idx < myArray.length) {
  console.log(myArray[idx]);
  idx++;
}
```

### for loop

```js
var myArray = ["Hello", 45, true];
for (var idx = 0; idx < myArray.length; idx++) {
  console.log(myArray[idx]);
}
```

Also nice little iterator for loop

```js
// for arrays, use of
var myArray = ["Hello", 45, true];
for (var val of myArray) {
  console.log(val);
}
// for objects, use in
var myObj = { myKey: "myValue", "my other key": 4 };
for (var key in myObj) {
  console.log(key, myObj[key]);
}
```

## Functions

```js
function myFunction(thing) {
  var hello = 3;
  world = 2;
  return thing.toUpperCase();
}
myFunction("foo");
// = FOO

// js has function scope
hello;
// = Uncaught ReferenceError: hello is not defined
world;
// = 2

// functions are first class objects
myObj = { custom: { whatever: myFunction } };
myObj.custom.whatever("yo");
// YO
```

### `this` is weird object self-reference

When functions attached to an object are called, they can access the object they're attached to using the `this` keyword.

```js
myObj = {
  myString: "Hello world!",
  myFunc: function () {
    return this.myString;
  },
};
myObj.myFunc();
// = 'Hello world!'
```

`this` depends on how function is called, not where it is defined.

```js
var myFunc = myObj.myFunc;
myFunc();

// = undefined
var myOtherFunc = function () {
  return this.myString.toUpperCase();
};
myObj.myOtherFunc = myOtherFunc;
myObj.myOtherFunc();
// = 'HELLO WORLD!'
```

### Constructor

`new` keyword means a new object is created and assigned to `this`.

```js
var MyConstructor = function () {
  this.myNumber = 5;
};
myNewObj = new MyConstructor();
myNewObj;
// = MyConstructor { myNumber: 5 }
```

## Prototypes

Vanilla JS has no classes. Instead it has prototypes which is inheritance and instantiation in one. Every object has a 'prototype'. When you access a property that doesn't exist on the actual object, the interpreter will look up in its prototype.

```js
var myObj = {
  myString: "Hello world!",
};
var myPrototype = {
  meaningOfLife: 42,
  myFunc: function () {
    return this.myString.toLowerCase();
  },
};
myObj.__proto__ = myPrototype;
myObj.meaningOfLife;
// = 42
myObj.myFunc();
// = 'hello world!'
```

You can set prototype of prototype too. Note how no copying is involved and modifying myPrototype is directly reflected.

```js
myPrototype.__proto__ = {
  myBoolean: true,
};
myObj.myBoolean;
// = true
```

`for/in` allows iteration inside prototypes. `hasOwnProperty` checks if key is object's property or 'inherited' from prototype.

```js
for (var x in myObj) {
  console.log(x, myObj[x], myObj.hasOwnProperty(x));
}
// = myString Hello world! true
// = meaningOfLife 42 false
// = myFunc [Function: myFunc] false
// = myBoolean true false
```

`__proto__` might not work in every js implementation. So, standard way of doing things is to add prototype property to constructors.

```js
var MyConstructor = function () {
  this.myName = 5;
};
MyConstructor.prototype = {
  myNumber: 5,
  getMyNumber: function () {
    return this.myNumber;
  },
};
var myNewObj2 = new MyConstructor();
myNewObj2.getMyNumber();
// = 6

// this creates new key in our object. Doesn't modify prototype
myNewObj2.myNumber = 6;
// yet this works, because of this magic
myNewObj2.getMyNumber();
// = 6
```
