# Yarn - Yet Another Resource Negotiator

Just like NPM, but [apparently was designed](https://www.geeksforgeeks.org/difference-between-npm-and-yarn/) to fix its performance and security concerns. There's not much difference really

[Install yarn](https://classic.yarnpkg.com/en/docs/install#mac-stable)


```
$ npm install --global yarn
```

## Usage

https://yarnpkg.com/getting-started/usage

Install all dependencies:  `yarn` or `yarn install`

```
$ yarn
yarn install v1.22.10
info No lockfile found.
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
[4/4] 🔨  Building fresh packages...
success Saved lockfile.
✨  Done in 2.41s.
```

Add a new dependecy

```
$ yarn add express
yarn add v1.22.10
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
[4/4] 🔨  Building fresh packages...
success Saved 1 new dependency.
info Direct dependencies
└─ express@4.17.1
info All dependencies
└─ express@4.17.1
✨  Done in 0.64s.
$ yarn add  prettier --dev
yarn add v1.22.10
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
[4/4] 🔨  Building fresh packages...

success Saved 1 new dependency.
info Direct dependencies
└─ prettier@2.3.1
info All dependencies
└─ prettier@2.3.1
✨  Done in 0.45s.
```

Yarn creates yarn.lock instead as opposed to npm's package-lock.json

## Scripts

Add scripts in package.json.

```
$ cat package.json 
{
  "name": "my_project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node index.js",
    "whatever": "echo \"whatever man, that's like your opinion\""
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

$ yarn start
yarn run v1.22.10
$ node index.js

$ yarn test
yarn run v1.22.10
$ echo "Error: no test specified" && exit 1
Error: no test specified
error Command failed with exit code 1.
info Visit https://yarnpkg.com/en/docs/cli/run for documentation about this command.
```

To run custom commands

```
$ yarn run whatever
yarn run v1.22.10
$ echo whatever man, that's like your opinion
whatever man, that's like your opinion
✨  Done in 0.05s.
```


