# xcmd

### A Boilerplate for Scalable Cross-Platform Desktop Apps

<br/>

[![Build Status][travis-image]][travis-url]
[![Appveyor Build Status][appveyor-image]][appveyor-url]
[![Dependency Status][david_img]][david_site]
[![Github Tag][github-tag-image]][github-tag-url]
[![Join the chat at https://gitter.im/xcmd/Lobby](https://badges.gitter.im/xcmd/Lobby.svg)](https://gitter.im/xcmd/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![OpenCollective](https://opencollective.com/xcmd/backers/badge.svg)](#backers)
[![OpenCollective](https://opencollective.com/xcmd/sponsors/badge.svg)](#sponsors)

[![React](/internals/img/react-padded-90.png)](https://facebook.github.io/react/)
[![Webpack](/internals/img/webpack-padded-90.png)](https://webpack.github.io/)
[![Redux](/internals/img/redux-padded-90.png)](http://redux.js.org/)
[![React Router](/internals/img/react-router-padded-90.png)](https://github.com/ReactTraining/react-router)
[![Flow](/internals/img/flow-padded-90.png)](https://flowtype.org/)
[![ESLint](/internals/img/eslint-padded-90.png)](http://eslint.org/)
[![Jest](/internals/img/jest-padded-90.png)](https://facebook.github.io/jest/)
[![Yarn](/internals/img/yarn-padded-90.png)](https://yarnpkg.com/)

[Electron](http://electron.atom.io/) application boilerplate based on [React](https://facebook.github.io/react/), [Redux](https://github.com/reactjs/redux), [React Router](https://github.com/reactjs/react-router), [Webpack](http://webpack.github.io/docs/), [React Transform HMR](https://github.com/gaearon/react-transform-hmr) for rapid application development.

## Screenshot

![Electron Boilerplate Demo](https://cloud.githubusercontent.com/assets/3382565/10557547/b1f07a4e-74e3-11e5-8d27-79ab6947d429.gif)

## Install

-   **Note: requires a node version >= 7 and an npm version >= 4.**
-   **If you have installation or compilation issues with this project, please see [our debugging guide](https://github.com/s-a/xcmd/issues/400)**

First, clone the repo via git:

```bash
git clone --depth=1 https://github.com/s-a/xcmd.git your-project-name
```

And then install dependencies with yarn.

```bash
$ cd your-project-name
$ yarn
```

**Note**: If you can't use [yarn](https://github.com/yarnpkg/yarn), run `npm install`.

## Run

Start the app in the `dev` environment. This starts the renderer process in [**hot-module-replacement**](https://webpack.js.org/guides/hmr-react/) mode and starts a webpack dev server that sends hot updates to the renderer process:

```bash
$ npm run dev
```

Alternatively, you can run the renderer and main processes separately. This way, you can restart one process without waiting for the other. Run these two commands **simultaneously** in different console tabs:

```bash
$ npm run start-renderer-dev
$ npm run start-main-dev
```

## Packaging

To package apps for the local platform:

```bash
$ npm run package
```

To package apps for all platforms:

First, refer to [Multi Platform Build](https://www.electron.build/multi-platform-build) for dependencies.

Then,

```bash
$ npm run package-all
```

To package apps with options:

```bash
$ npm run package -- --[option]
```

To run End-to-End Test

```bash
$ npm run build
$ npm run test-e2e
```

:bulb: You can debug your production build with devtools by simply setting the `DEBUG_PROD` env variable:

```bash
DEBUG_PROD=true npm run package
```

## How to add modules to the project

You will need to add other modules to this boilerplate, depending on the requirements of your project. For example, you may want to add [node-postgres](https://github.com/brianc/node-postgres) to communicate with PostgreSQL database, or 
[material-ui](http://www.material-ui.com/) to reuse react UI components.

⚠️ Please read the following section before installing any dependencies ⚠️

### Module Structure

This boilerplate uses a [two package.json structure](https://github.com/electron-userland/electron-builder/wiki/Two-package.json-Structure). This means, you will have two `package.json` files.

1.  `./package.json` in the root of your project
2.  `./app/package.json` inside `app` folder

### Which `package.json` file to use

**Rule of thumb** is: all modules go into `./package.json` except native modules. Native modules go into `./app/package.json`.

1.  If the module is native to a platform (like node-postgres) or otherwise should be included with the published package (i.e. bcrypt, openbci), it should be listed under `dependencies` in `./app/package.json`.
2.  If a module is `import`ed by another module, include it in `dependencies` in `./package.json`.   See [this ESLint rule](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-extraneous-dependencies.md). Examples of such modules are `material-ui`, `redux-form`, and `moment`.
3.  Otherwise, modules used for building, testing and debugging should be included in `devDependencies` in `./package.json`.

### Further Readings

See the wiki page, [Module Structure — Two package.json Structure](https://github.com/s-a/xcmd/wiki/Module-Structure----Two-package.json-Structure) to understand what is native module, the rationale behind two package.json structure and more.

For an example app that uses this boilerplate and packages native dependencies, see [erb-sqlite-example](https://github.com/amilajack/erb-sqlite-example).

## CSS Modules

This boilerplate is configured to use [css-modules](https://github.com/css-modules/css-modules) out of the box.

All `.css` file extensions will use css-modules unless it has `.global.css`.

If you need global styles, stylesheets with `.global.css` will not go through the
css-modules loader. e.g. `app.global.css`

If you want to import global css libraries (like `bootstrap`), you can just write the following code in `.global.css`:

```css
@import "~bootstrap/dist/css/bootstrap.css";
```

## Sass support

If you want to use Sass in your app, you only need to import `.sass` files instead of `.css` once:

```js
import './app.global.scss';
```

## Static Type Checking

This project comes with Flow support out of the box! You can annotate your code with types, [get Flow errors as ESLint errors](https://github.com/amilajack/eslint-plugin-flowtype-errors), and get [type errors during runtime](https://github.com/codemix/flow-runtime) during development. Types are completely optional.

## Dispatching redux actions from main process

See [#118](https://github.com/s-a/xcmd/issues/118) and [#108](https://github.com/s-a/xcmd/issues/108)

## How to keep your project updated with the boilerplate

If your application is a fork from this repo, you can add this repo to another git remote:

```sh
git remote add upstream https://github.com/s-a/xcmd.git
```

Then, use git to merge some latest commits:

```sh
git pull upstream master
```

[npm-image]: https://img.shields.io/npm/v/xcmd.svg?style=flat-square

[github-tag-image]: https://img.shields.io/github/tag/s-a/xcmd.svg

[github-tag-url]: https://github.com/s-a/xcmd/releases/latest

[travis-image]: https://travis-ci.org/s-a/xcmd.svg?branch=master

[travis-url]: https://travis-ci.org/s-a/xcmd

[appveyor-image]: https://ci.appveyor.com/api/projects/status/github/s-a/xcmd?svg=true

[appveyor-url]: https://ci.appveyor.com/project/s-a/xcmd/branch/master

[david_img]: https://img.shields.io/david/s-a/xcmd.svg

[david_site]: https://david-dm.org/s-a/xcmd
