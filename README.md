# Jade Static Loader

[![npm](http://img.shields.io/npm/v/jade-static-loader.svg?style=flat)](https://badge.fury.io/js/jade-static-loader) [![tests](http://img.shields.io/travis/static-dev/jade-static-loader/master.svg?style=flat)](https://travis-ci.org/static-dev/jade-static-loader) [![dependencies](http://img.shields.io/david/static-dev/jade-static-loader.svg?style=flat)](https://david-dm.org/static-dev/jade-static-loader)
[![coverage](http://img.shields.io/coveralls/static-dev/jade-static-loader.svg?style=flat)](https://coveralls.io/github/static-dev/jade-static-loader)

Webpack loader that compiles jade to static html

> **Note:** This project is in early development, and versioning is a little different. [Read this](http://markup.im/#q4_cRZ1Q) for more details.

### Why should you care?

This loader is intended to be used in situations where you want webpack to render a static html file rather than a client side template. It's written by the authors of [spike](https://github.com/static-dev/spike), a static website engine with webpack at the core.

If you are looking for a simple, solid, and well maintained webpack loader that renders out jade as html, you have come to the right place.

### Installation

`npm i jade-static-loader -S`

### Usage

This loader does not accept any options via `query`, because all `query` options are stringified, which means that functions cannot be passed. However, it's quite a common use-case to pass a function to jade as a local, and unfortunately functions cannot be stringified. Also querystrings are ugly.

So instead, this loader pulls settings directly from the webpack options, from the `jade` key. If you were to set up a simple webpack project using this loader, it would look something like this:

```js
// webpack.config.js
module.exports = {
  module: {
    loaders: [
      { test: /\.jade$/, loader: 'jade-static' }
    ]
  },
  jade: {
    pretty: false,
    locals: { foo: 'bar' }
  }
}
```

The loader simply returns an export of a string containing the compiled html. Now you also probably would want to extract out the resulting code and write it to an html file, rather than letting it chill in your javascript output, but that's not part of what a loader can do, so use some plugins or maybe spike for this instead.

This loader also exposes the source of the original jade files internally for plugins to access, using the `_src` property of each webpack module object.

### License & Contributing

- Details on the license [can be found here](LICENSE.md)
- Details on running tests and contributing [can be found here](contributing.md)
