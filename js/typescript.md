---
parent: JavaScript
nav_order: 4
---

# TypeScript

JavaScript is not typed: you can pass object to a function that expects list and there'll be no error until the code is run. What this means is that your code can be 'unsafe' with errors that are only apparent during run time. TypeScript aims to solve this problem by introducing type safety to JS like C++ or Java. TypeScript is a super set of JS. Therefore, all JS code is valid TypeScript code. Let's review the TypeScript extra syntax here. [Reference](https://learnxinyminutes.com/docs/typescript/)

Install TypeScript to your project:

```bash
$ npm install typescript --save-dev
$ touch hello.ts
$ npx tsc hello.ts
# hello.ts is compiled to hello.js
$ cat hello.js
```

## Basic Types

There are 3 basic types in TypeScript

```ts
let isDone: boolean = false;
let lines: number = 42;
let name: string = "Anders";
```

But you can omit the type annotation if the variables are derived from explicit literals

```ts
let isDone = false;
let lines = 42;
let name = "Anders";
```

If you try to assign a number to boolean, `tsc` raises an error.

```ts
// hello.ts
let isDone = false;
isDone = 2;
```

```bash
$ npx tsc hello.ts
hello.ts:2:1 - error TS2322: Type 'number' is not assignable to type 'boolean'.

2 isDone = 2
  ~~~~~~


Found 1 error.
```

You can use `any` type for the variables you want to resign:

```ts
let notSure: any = 4;
notSure = "maybe a string instead";
```

You can have enumerations

```ts
enum Color {
  Red,
  Green,
  Blue,
}
let c: Color = Color.Green;
```

## Functions

You can annotate the function outputs types as follows. Here `void` is used because function returns nothing.

```ts
function bigHorribleAlert(): void {
  alert("I'm a little annoying box!");
}
```

Functions will also try inferring the output type.

```ts
let fn = function (i: number) {
  return i * i;
};
```

Also here's how you use arrow syntax for functions

```ts
let fn = (i: number): number => {
  return i * i;
};
```

## Interfaces

Similar to classes but you don't have implementation in the declaration. Anything that has the properties is compliant with the interface

```ts
interface Person {
  name: string;
  // Optional properties, marked with a "?"
  age?: number;
  // And of course functions
  move(): void;
}

// p is valid Person
let p: Person = { name: "Bobby", move: () => {} };

// but since there's no move here, this is an invalid Person.
// compiler will raise an error.
let invalidPerson: Person = { name: "Bobby", age: 20 };
```

You can also have interfaces for functions

```ts
interface SearchFunc {
  (source: string, subString: string): boolean;
}
let mySearch: SearchFunc;
mySearch = function (src: string, sub: string) {
  return src.search(sub) != -1;
};
```

## Classes

All members are public by default.

```js
class Point {
  // Properties
  x: number;

  // Constructor - the public/private keywords in this context will generate
  // the boiler plate code for the property and the initialization in the
  // constructor.
  // In this example, "y" will be defined just like "x" is, but with less code
  // Default values are also supported

  constructor(x: number, public y: number = 0) {
    this.x = x;
  }

  // Functions
  dist(): number { return Math.sqrt(this.x * this.x + this.y * this.y); }

  // Static members
  static origin = new Point(0, 0);
}

let p1 = new Point(10, 20);
```

You can also have classes implementing an interface

```ts
class PointPerson implements Person {
  name: string;
  move() {}
}
```

Inheritance is done using `extends` keyword

```ts
class Point3D extends Point {
  constructor(x: number, y: number, public z: number = 0) {
    super(x, y); // Explicit call to the super class constructor is mandatory
  }

  // Overwrite
  dist(): number {
    let d = super.dist();
    return Math.sqrt(d * d + this.z * this.z);
  }
}
```

## Modules

You can use modules for name spacing

```ts
module Geometry {
  export class Square {
    constructor(public sideLength: number = 0) {
    }
    area() {
      return Math.pow(this.sideLength, 2);
    }
  }
}

let s1 = new Geometry.Square(5);

// Local alias for referencing a module
import G = Geometry;

let s2 = new G.Square(10);
```