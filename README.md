# ⚛ React-Express–TypeScript-SSR Setup

**Advertising**: I wrote a book about React. There's a German and an English version. Buy one if you like this project and you want to support my work!

**New!** You can now use this project as template!

## TOC

- [Motivation]
- [Goals]
- [Features]
- [Installation]
- [Usage]
- [Tricks]
  - [Client side version (opt-in)]
  - [Component scaffolding using plop]
  - [📕 Storybook support]
  - [Keep your project up to date]
  - [Avoid source map generation for faster builds]
  - [Change the port of the dev environment]
  - [Import SVGs as ReactComponent]
  - [Use plain JavaScript instead of TypeScript]
- [Caveats]
- [Todo]
- [Changelog]

## Motivation

This is just another React Starter Project as there are literally [hundreds of others out there]. The reason I created this one was to have one central repo I can base my own future projects on, which contains most of the packages I usually use, is easily extendable, easy to understand, supports server side rendering, and uses all the configs and settings I made good experiences with in the past.

Another reason I created my own starter project was because I was setting up two new long term projects and I wanted to be able to use **Webpack 4** and **Babel 7** long before it was stable. None of the bigger and well known starter projects were supporting both by the time I created this starter project. So the idea was born to create my very own. And here we are 🎉

A few things might be familiar when you've worked with other starter projects before. I borrowed many ideas (and will continue to do so) from [Create React App], [React Starter Kit] and other great starter projects because my intention was to create an **up-to-date starter project** for myself **based on best practices** and not to completely reinvent the wheel in every possible way just for the sake of it.

## Goals

My goal is to provide a **well-tested, regularly maintained, easily configurable and adjustable React Starter Project** with support for server side rendering that gives you a good basis to start your own project on. As minimal as possible with as much functionality as necessary.

I use this Starter Project in several real-word projects so it is battle-tested and everytime I fix a bug or add a feature I find useful I will also update this Starter Project. I will also keep the dependencies up-to-date on a regular basis and will also stay updated with all the latest and greatest best practices in the React world and integrate them if possible and useful!

If you have any questions you can always [open an issue on Github] or reach out to me on [Twitter]!

## Features

This project has out-of-the-box support for the following things:

- General Setup

  - 🔥 Babel 7
  - 📦 Webpack 4
  - 🔥 ESLint 7 (with a set of custom rules which may be mostly identical to AirBnB with some personal flavor added)
  - 🔥 TypeScript (via Babel)
  - 🔥 Prettier
  - 🔥 Jest
  - 🐐 React Testing Library
  - ✅ React i18next for multi language support
  - ✅ Server Side Rendering with Express
  - 🏎 React Fast Refresh
  - ✅ CSS Modules
  - ✅ PostCSS
  - ✅ Precommit hooks via lint-staged + Husky
  - ✅ Optional static build without the need for Node.js on the server
  - 📕 Support for [Storybook](https://storybook.js.org/) (>= 5.0.0)

- Libs and Dependencies

  - ✅ React i18next for multi language support
  - ⚛ React 16.x (latest), with Hooks!
  - ✅ Redux + Thunk middleware
  - ✅ Immer
  - ✅ Reselect
  - ✅ React Router 5
  - ✅ React Helmet

Since it's only using standard APIs so far it is ready to be used with the new React Suspense feature coming in React 17!

## Installation

As a general recommendation you should create a **fork** of this project first or use GitHub's [use this template] function so you can adjust it to your own needs, add all the dependencies you need and commit everything back into your own repository.

Once you've forked the repository here on Github, clone it, `cd` into the directory and run `yarn` (or `npm install`) on your command line to install all the dependencies. You're ready to go now!

## Usage

There are npm scripts for all the relevant things. The server will always be started on port 8500 unless otherwise specified in `process.env.PORT`. You can use a `.env` file to specify env vars. If you want to use them in your client side code, don't forget to add them in [config/env.js]

### Noteworthy scripts:

#### `yarn start`

Starts the app in development mode: creates a new client and server dev build using webpack, starts the Express server build (for both file serving and server side pre-rendering) and keeps webpack open in watchmode. Updates the app (if possible) on change using HMR.

#### `yarn build`

Creates a new build, optimized for production. Does **not** start a dev server or anything else.

#### `yarn test`

Run all tests using jest.

#### `yarn test:update`

Update all Jest snapshots (if there are any)

#### `yarn lint:js`

Run ESLint for all JavaScript and TypeScript files

#### `yarn lint:css`

Run Stylelint for all CSS files

#### `yarn lint`

Run lint:js and lint:css in parallel

#### `yarn analyze`

Starts `webpack-bundle-analyzer` to give you the opportunity to analyze your bundle(s)

#### `yarn depgraph`

Creates an image of your dependency graph. Requires [GraphVIZ] to be in your system's `PATH`

#### `yarn plop`

Run plop to create new React components or Redux reducers via CLI

## Environment Variables

There are a few environment variables you can set to adjust the setup to your needs

| Variable         | Default            | Description                                                                                                                                                                                                                                                                                      |
| ---------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `PORT`           | `8500`             | Port number your application will be served on.                                                                                                                                                                                                                                                  |
| `HOST`           | `http://localhost` | Host (including protocol!) your application will be served on. This is usually neglectable as most of the time your application will be served via remote proxy (e.g. Nginx) on localhost. **Note:** this is only for convenience. The server itself will not be bound exclusively to that host. |
| `DEVSERVER_HOST` | `http://localhost` | Optional. Different host for the Webpack Dev Server to be served on.                                                                                                                                                                                                                             |

## Tricks

### Client side version (opt-in)

Beginning with v1.3.0, a **static** `index.html` is also generated and written to your `clientBuild` directory. You are now able to deploy the `build/client` directory to a static webhost (such as Netlify or AWS S3) and serve your application from there!

For the generation of the `index.html` the server side build gets started right after building, a headless Chrome then visits the site and writes the content of the server side response to your client directory. So you still need the `src/server` directory and the server side build but you're now flexible and can decide on your own whether you want to have the full server side experience or only deploy your completely static app somewhere.

### Component scaffolding using plop

Along with this starter kit comes `plop` - a great command line tool to keep the structure of your Redux components and Redux reducers consistent. Run `yarn plop` (or `npm run plop`) to have components and Redux reducers created for you automatically! Just enter a name, answer a few questions and you're ready to go! You can of course adjust everything to your needs. All Plop templates can be found in the `config/plop` directory.

### 📕 Storybook support

I've successfully tested Storybook and it integrates seamlessly and without any issues into this setup. If you want to add Storybook to your project, install Storybook `^4.0.0` and run `getstorybook` to have the basic setup created for you. You must then replace all the content in `.storybook/webpack.config.js` with the following line:

```js
module.exports = require('../config/webpack.config.js/storybook');
```

Afterwards you should be able to run `yarn storybook` to start the Storybook Dev Server.

### Keep your project up to date

If you want _your_ project to stay up to date with recent changes to _this_ project, you can add **React SSR Starter** as remote to your local git repo. Use the following line:

```
git remote add upstream git@github.com:manuelbieh/react-ssr-setup.git
```

More on that can be found on Github: [Syncing a fork].

### Avoid source map generation for faster builds

In some cases you might not want to generate source maps for the generated files. In this case you can set the `OMIT_SOURCEMAP` environment variable to `true`. No source map files will be generated then. This works no matter if you're in devmode or building for production.

### Change the port of the dev environment

By default if you run `yarn start` the development server will use port 8500. You can change this by specifying a `PORT` environment variable.

### Import SVGs as ReactComponent

You can import SVG files as React components exactly the way you can do it in Create React App 2.0:

```
import { ReactComponent as Logo } from './Logo.svg';
```

Then you can use it in JSX like `<div><Logo /></div>`.

<!--
### Managing i18n translation files

_(WIP: this is not quite working, yet!)_

This project comes with i18n support out of the box. It's using i18next and react-i18next to provide comprehensive tooling and mechanisms to translate your app. Additionally I've started to add support for translation management for external online translation services (currently lokalise.co is the only available provider). You can use the Lokalise web interface to handle all your translations, export them to use them in your app and also import them from your app via a simple `yarn i18n:push`.

You have to define two new env variables to be able to import/export translations to/from Lokalise: `LOKALISE_TOKEN` and `LOKALISE_PROJECT_ID`. Afterwards you can create new translations via their web interface or collect all static translation strings from your app using `yarn i18n:scan` and then push them to Lokalise using `yarn i18n:push`.
-->

<!--
This following section is no longer fully true since I decided to go all-in on TypeScript. I leave it in here for now for historical reasons.

### Use plain JavaScript instead of TypeScript

You can just do it‬™. Really. Name your files `.js` instead of `.ts`/`.tsx` and you should not be bothered by TypeScript anymore. If you want to _fully_ remove TypeScript:

- remove the `@babel/typescript` preset from `babel.config.js`
- uninstall TypeScript: `yarn remove typescript @babel/preset-typescript`
- uninstall all dependencies beginning with `@types/`
- delete `tsconfig.json` and `src/global.d.ts`
- remove `wiremore/typescript` from the `extends` section in `.eslintrc.js`
- remove all types from all files if there still are any
- remove `tsConfig` option from `.dependency-cruiser.js`
-->

### Contacts

![Gmail](https://github.com/santaclous112/MonilP-Portfolio/blob/master/src/components/Icon/svg/mailto.svg)               
        santaclous112@gmail.com

![Skype](https://github.com/santaclous112/MonilP-Portfolio/blob/master/src/components/Icon/svg/skype.svg)               
        live:.cid.772f958a47f37977

![Telegram](https://github.com/santaclous112/MonilP-Portfolio/blob/master/src/components/Icon/svg/telegram.svg)               
        PeaceStar01
