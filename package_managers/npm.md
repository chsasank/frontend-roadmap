---
parent: Package Managers
nav_order: 1
---

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

## Dependencies

```
$ npm install express
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN my_project@1.0.0 No description
npm WARN my_project@1.0.0 No repository field.

+ express@4.17.1
added 50 packages from 37 contributors and audited 50 packages in 4.266s
found 0 vulnerabilities
```

Note the creation of package-lock.json. It is there to allow reproduction of exact builds. Also see how dependencies is added to package.json

```
$ ls
index.js                node_modules            package-lock.json       package.json
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
  "license": "ISC",
  "dependencies": {
    "express": "^4.17.1"
  }
}
```

You can also install dev only dependencies

```
$ npm install --save-dev prettier
npm WARN my_project@1.0.0 No description
npm WARN my_project@1.0.0 No repository field.

+ prettier@2.3.1
added 1 package from 1 contributor and audited 51 packages in 1.676s
found 0 vulnerabilities

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
  "license": "ISC",
  "dependencies": {
    "express": "^4.17.1"
  },
  "devDependencies": {
    "prettier": "^2.3.1"
  }
}
```

You can also install global packages (i.e. not restricted to this project)

```
$ npm install -g eslint
$ npm install -g eslint
/Users/sasank/.nvm/versions/node/v14.17.0/bin/eslint -> /Users/sasank/.nvm/versions/node/v14.17.0/lib/node_modules/eslint/bin/eslint.js
+ eslint@7.28.0
added 116 packages from 68 contributors in 6.895s
$ cd ~
$ $ eslint --version
v7.28.0
```

You can also publish packages to npm server, but that's for another day.
