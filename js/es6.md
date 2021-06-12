---
parent: JavaScript
nav_order: 3
---

# ECMAScript or ES6

ECMAScript or ES are revisions to javascript language. ES6 is the most important revision we need to know about. Here are some of the important new features added in ES6. [Reference](https://www.w3schools.com/js/js_es6.asp)

## Variable declarations: `let` and `const`

`let` allows you to declare with block scope. Remember that `var` has function scope. `const` is similar to `let` but value can't be changed.

```js
{
  var x = 5;
  let y = 3;
  const z = 3;
}
x;
// = 5
y;
// = undefined
z;
// = 3
z = 5;
// = Uncaught TypeError: Assignment to constant variable.
```

## Functions

Arrow functions are shorter syntax for writing functions. All the below are equivalent.

```js
// ES5
var fn1 = function (x, y) {
  return x * y;
};

// ES6
const fn2 = (x, y) => x * y;
const fn3 = (x, y) => {
  return x * y;
};
```

Functions can now have default parameter values

```js
function myFunction(x, y = 10) {
  // y is 10 if not passed or undefined
  return x + y;
}
myFunction(5);
// = 15
```

Can have unlimited number of parameters as well

```js
function sum(...args) {
  let sum = 0;
  for (let arg of args) sum += arg;
  return sum;
}

sum(4, 9, 16, 25, 29, 100, 66, 77);
// = 326
```

## Classes

Finally, JS now has classes!

```js
class Car {
  constructor(name, year) {
    this.name = name;
    this.year = year;
  }

  getName() {
    return this.name.toUpperCase();
  }
}
const myCar1 = new Car("Ford", 2014);
const myCar2 = new Car("Audi", 2019);
myCar2.getName();
// = 'AUDI'
```

## Promises

A JavaScript Promise object contains both the producing code and calls to the consuming code.

```js
const myPromise = new Promise(function (resolve, reject) {
  // "Producing Code" (May take some time)

  let rand = Math.random();
  if (rand > 0.5) {
    // success
    setTimeout(function () {
      resolve("I love you, but I'm late");
    }, 1000);
  } else {
    // error
    setTimeout(() => reject(["I hate you", rand]));
  }
});

// consuming code
myPromise.then(
  (msg) => {
    console.log(`success msg = ${msg}`);
  },
  ([msg, reason]) => {
    console.log(`error msg = ${msg} because rand = ${reason}`);
  }
);
// 50% of time (after 1 seconds)
// = success msg = I love you, but I'm late
// 50% of time (immediately)
// = error msg = I hate you because rand = 0.13482
```
