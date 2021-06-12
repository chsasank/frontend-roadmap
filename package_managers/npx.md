---
parent: Package Managers
nav_order: 3
---

# NPX - Node.js Package Runner

Gotta love [freecodecamp](https://www.freecodecamp.org/news/npm-vs-npx-whats-the-difference/) for great tutorial.

npx is bundled with npm, so no installation required.
```
$ which npx
/Users/sasank/.nvm/versions/node/v14.17.0/bin/npx
```

## Why do you need npx anyway?

Say you installed prettier, the awesome js file formatter.

```
$ yarn add prettier --dev
yarn add v1.22.10
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
[4/4] 🔨  Building fresh packages...

success Saved lockfile.
success Saved 1 new dependency.
info Direct dependencies
└─ prettier@2.3.1
info All dependencies
└─ prettier@2.3.1
✨  Done in 0.50s.
```

But you can't use prettier because it's not in your path

```
$ prettier index.js 
-bash: prettier: command not found
```

npx solves this problem! Just prefix your command with npx

```
$ npx prettier index.js 
const http = require("http");

const requestListener = function (req, res) {
  res.writeHead(200);
  res.end("Hello, World!");
};

const server = http.createServer(requestListener);
server.listen(8080);
```

Heck, you can run without even adding the package to dependencies. Well-known example is CRA (create-react-app):

```
$ npx create-react-app --help
npx: installed 67 in 3.173s
Usage: create-react-app <project-directory> [options]

Options:
  -V, --version                            output the version number
  --verbose                                print additional logs
  --info                                   print environment debug info
  --scripts-version <alternative-package>  use a non-standard version of react-scripts
  --template <path-to-template>            specify a template for the created project
  --use-npm                                
  --use-pnp                                
  -h, --help                               output usage information
    Only <project-directory> is required.

    A custom --scripts-version can be one of:
      - a specific npm version: 0.8.2
      - a specific npm tag: @next
      - a custom fork published on npm: my-react-scripts
      - a local path relative to the current working directory: file:../my-react-scripts
      - a .tgz archive: https://mysite.com/my-react-scripts-0.8.2.tgz
      - a .tar.gz archive: https://mysite.com/my-react-scripts-0.8.2.tar.gz
    It is not needed unless you specifically want to use a fork.

    A custom --template can be one of:
      - a custom template published on npm: cra-template-typescript
      - a local path relative to the current working directory: file:../my-custom-template
      - a .tgz archive: https://mysite.com/my-custom-template-0.8.2.tgz
      - a .tar.gz archive: https://mysite.com/my-custom-template-0.8.2.tar.gz

    If you have any problems, do not hesitate to file an issue:
      https://github.com/facebook/create-react-app/issues/new

```