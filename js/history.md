# History of Javascript (until 2017)

[Reference](https://medium.com/the-node-js-collection/modern-javascript-explained-for-dinosaurs-f695e9747b70). This page is my notes of the article.

## Old school way

Javascript first appeared in 1995. Old school way is to use a script tag, just like image in html.

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>JavaScript Example</title>
    <script src="index.js"></script>
  </head>
  <body>
    <h1>Hello from HTML!</h1>
  </body>
</html>
```

```js
// index.js
console.log("Hello from JavaScript!");
```

If you wanted to install a library like [moment.js](https://momentjs.com/), you would download `moment.min.js` (`min` for minified or compressed) and add following line in `header` of html:

```html
<script src="moment.min.js"></script>
```

and in your index.js

```js
console.log(moment().startOf("day").fromNow());
```

This is easy to understand, but painful to maintain because you've to manually maintain versions.

## Enter npm

There were several competing JS package managers starting 2010. Bower was popular until 2013. npm overtook it in 2015. Yarn picked up steam in 2016, but it's just an alternate interface to npm.

npm is package manager for node.js but that didn't stop people from using it for front end. See `package_managers/npm.md` for detailed notes on npm. Here's some basic use:

```js
// creates package.json
$ npm init
// add your dependency. updates package.json
$ npm install moment --save
```

your library is downloaded to `node_modules`. Use it in your html:

```html
<script src="node_modules/moment/min/moment.min.js"></script>
```

Now npm takes care of downloading and updating packages. But it's still a hassle because you've to put path manually.

## webpack: module bundler

Most programming languages have `import` or `include` something like that but js originally didn't have it. This meant libraries had to share a global variable which is available for all the files loaded later.

In 2009, a project named CommonJS was started with a goal to make JS runtime come out of browser closet. Figuring out import and export was big part of this project. Node.js is most well known implementation of the project!

This is how you do it in node. Since node has access to computer's file system, it knows and loads the path to the exact js file of moment library.

```js
// index.js
var moment = require('moment');

console.log("Hello from JavaScript!");
console.log(moment().startOf('day').fromNow());
```

But this won't work on browser because browsers are designed to get no file access. We need a module bundler to replace all the require statements with actual file contents. Result is one single bundled JS file.

In 2011, browersify was the most popular bundler. But in 2015, webpack became the more widely used bundler, fueled by popularity of react, a front end framework. Here's how install webpack:

```bash
# --save-dev means development dependencies
$ npm install webpack webpack-cli --save-dev
```

This create bundle in dist/main.js

```bash
./node_modules/.bin/webpack index.js 
```

This bundle is the only file you add in your html header!

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript Example</title>
  <script src="dist/main.js"></script>
</head>
<body>
  <h1>Hello from HTML!</h1>
</body>
</html>
```

Tip: you can use npm scripts to make this even simpler to use!