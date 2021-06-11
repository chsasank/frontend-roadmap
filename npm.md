# NPM - Node Package Manager

A great reference: https://www.freecodecamp.org/news/what-is-npm-a-node-package-manager-tutorial-for-beginners/

NPM is like pip for python or gem for ruby.


## Package.json

```bash
$ mkdir my_project
$ cd my_project/
$ npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help init` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (my_project) 
version: (1.0.0) 
description: 
entry point: (index.js) 
test command: 
git repository: 
keywords: 
author: 
license: (ISC) 
About to write to /Users/sasank/projects/qure/frontend-dev/npm/my_project/package.json:

{
  "name": "my_project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}


Is this OK? (yes) yes
$ ls
package.json
```

## Scripts

Run your scripts

```bash
$ cat package.json 
{
  "name": "my_project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node index.js"
  },
  "author": "",
  "license": "ISC"
}
$ cat index.js 
const http = require('http');

const requestListener = function (req, res) {
  res.writeHead(200);
  res.end('Hello, World!');
}

const server = http.createServer(requestListener);
server.listen(8080);
$ npm start

> my_project@1.0.0 start /Users/sasank/projects/qure/frontend-dev/npm/my_project
> node index.js

```
