<div align="center">
  <!-- replace with accurate logo e.g from https://worldvectorlogo.com/ -->
  <a href="https://github.com/webpack/webpack">
    <img width="200" height="200" vspace="" hspace="25"
      src="https://cdn.rawgit.com/webpack/media/e7485eb2/logo/icon.svg">
  </a>
  <h1>NPM Install Webpack Plugin</h1>
  <p>Speed up development by <b>automatically installing & saving dependencies</b> with Webpack.<p>
</div>

It sucks to <kbd>Ctrl-C</kbd> your
build script & server just to install
a dependency you didn't know you needed until now.

Instead, use `require` or `import` how you normally would and `npm install`
will happen **automatically to install & save missing dependencies** while you work!

<h2 align="center">Install</h2>

```bash
$ npm install --save-dev npm-install-webpack-plugin
```

<h2 align="center">Usage</h2>

In your `webpack.config.js`:

```js
plugins: [
  new NpmInstallPlugin()
],
```

**This is equivalent to**:

```js
plugins: [
  new NpmInstallPlugin({
    // Use --save or --save-dev
    dev: false,
    // Install missing peerDependencies
    peerDependencies: true,
    // Reduce amount of console logging
    quiet: false,
    // npm command used inside company, yarn is not supported yet
    npm: 'tnpm'
  });
],
```

You can provide a `Function` to the `dev` to make it dynamic:

```js
plugins: [
  new NpmInstallPlugin({
    dev: function(module, path) {
      return [
        "babel-preset-react-hmre",
        "webpack-dev-middleware",
        "webpack-hot-middleware",
      ].indexOf(module) !== -1;
    },
  }),
],
```

<h2 align="center">Demo</h2>

![npm-install-webpack-plugin demo](https://cloud.githubusercontent.com/assets/15182/12540538/6a4e8f1a-c2d0-11e5-97ee-4ddaf6892645.gif)

<h2 align="center">Features</h2>

- [x] Works with both Webpack `^v1.12.0` and `^2.1.0-beta.0`.
- [x] Auto-installs `.babelrc` plugins & presets.
- [x] Supports both ES5 & ES6 Modules.
  (e.g. `require`, `import`)
- [x] Supports Namespaced packages.
  (e.g. `@cycle/dom`)
- [x] Supports Dot-delimited packages.
  (e.g. `lodash.capitalize`)
- [x] Supports CSS imports.
  (e.g. `@import "~bootstrap"`)
- [x] Supports Webpack loaders.
  (e.g. `babel-loader`, `file-loader`, etc.)
- [x] Supports inline Webpack loaders.
  (e.g. `require("bundle?lazy!./App"`)
- [x] Auto-installs missing `peerDependencies`.
  (e.g. `@cycle/core` will automatically install `rx@*`)
- [x] Supports Webpack's `resolve.alias` & `resolve.root` configuration.
  (e.g. `require("react")` can alias to `react-lite`)
