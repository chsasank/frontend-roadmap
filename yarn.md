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

