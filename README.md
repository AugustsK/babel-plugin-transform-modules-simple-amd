# babel-plugin-transform-modules-simple-amd-with-default-exports [![npm version](https://badge.fury.io/js/babel-plugin-transform-modules-simple-amd-with-default-exports.svg)](https://badge.fury.io/js/babel-plugin-transform-modules-simple-amd-with-default-exports)

Limited transformer for ECMAScript 2015 (and beyond) modules into simplified AMD format.

Converts this code:
```js
import x from '/path/to/x';
import y from '/path/to/y';
doSomething();
export default x + y;
```

Into this one:
```js
define(['/path/to/x', '/path/to/y'], function (x, y) {
  doSomething();
  return x + y;
});
```

Instead of this one (generated with ``@babel/plugin-transform-modules-amd``):
```js
define(['exports', '/path/to/x', '/path/to/y'], function (exports, _x, _y) {
  Object.defineProperty(exports, "__esModule", {
    value: true
  });

  var _x2 = _interopRequireDefault(_x);

  var _y2 = _interopRequireDefault(_y);

  function _interopRequireDefault(obj) {
    return obj && obj.__esModule ? obj : {
      'default': obj
    };
  }

  doSomething();
  exports.default = _x2.default + _y2.default;
});
```

Forked from this PR that never got merged in: https://github.com/finom/babel-plugin-transform-es2015-modules-simple-amd/pull/10

## Installation

```sh
$ npm install -D babel-plugin-transform-modules-simple-amd-with-default-exports
```

## Usage

### Via `.babelrc` (Recommended)

**.babelrc**

```json
{
  "plugins": ["babel-plugin-transform-modules-simple-amd-with-default-exports"]
}
```

### Via Node API

```javascript
require('babel').transform('code', {
  plugins: ['babel-plugin-transform-modules-simple-amd-with-default-exports']
});
```

[The same thing for CommonJS](https://github.com/finom/babel-plugin-transform-es2015-modules-simple-commonjs).

Thanks to [finom](https://github.com/finom/babel-plugin-transform-es2015-modules-simple-amd) and [dcleao](https://github.com/finom/babel-plugin-transform-es2015-modules-simple-amd/pull/10).
