# license-info-webpack-plugin

[![npm version](https://badge.fury.io/js/license-info-webpack-plugin.svg)](https://www.npmjs.com/package/license-info-webpack-plugin)
![](https://github.com/yami-beta/license-info-webpack-plugin/workflows/ci/badge.svg)

`license-info-webpack-plugin` is a webpack plugin for making a list of package's LICENSE information, inspired by [licensify](https://github.com/twada/licensify).

```sh
$ npm install --save-dev license-info-webpack-plugin
```

```sh
$ yarn add --dev license-info-webpack-plugin
```

## Usage

### webpack v4

If you use `webpack < 4.2` that has dependency on `uglifyjs-webpack-plugin < 1.2.4`, you need to set `optimization` to set `uglifyOptions`.

```js
const path = require('path');
const LicenseInfoWebpackPlugin = require('license-info-webpack-plugin').default;
const UglifyJsPlugin = require("uglifyjs-webpack-plugin");

module.exports = {
  mode: 'production',
  entry: './src/js/index.js',
  output: {
    path: path.join(__dirname, 'dist/js'),
    filename: '[name].js'
  },
  plugins: [
    new LicenseInfoWebpackPlugin({
      glob: '{LICENSE,license,License}*'
    })
  ]
};
```

### webpack v3

```js
const path = require('path');
const LicenseInfoWebpackPlugin = require('license-info-webpack-plugin').default;
const UglifyJsPlugin = require("uglifyjs-webpack-plugin");

module.exports = {
  entry: './src/js/index.js',
  output: {
    path: path.join(__dirname, 'dist/js'),
    filename: '[name].js'
  },
  plugins: [
    new LicenseInfoWebpackPlugin({
      glob: '{LICENSE,license,License}*'
    }),
    new UglifyJsPlugin({
      uglifyOptions: {
        output: {
          comments: /^\**!|@preserve|@license|@cc_on/
        }
      }
    })
  ]
};
```

### Note

If you use `uglifyjs-webpack-plugin@^1.2.4` or `webpack` has dependency on `uglifyjs-webpack-plugin@^1.2.4`, you **don't need to set `uglifyOptions`** for preserve license comments.  
Related: https://github.com/webpack-contrib/uglifyjs-webpack-plugin/pull/250

If you use `uglifyjs-webpack-plugin@~1.1`, you need to set `uglifyOptions` for preserve license comments.  
Related: https://github.com/webpack-contrib/uglifyjs-webpack-plugin/pull/174

`license-info-webpack-plugin` needs `webpack v3.0 or above`

### Options

- `glob`
    - Glob pattern for LICENSE file
    - Default: `'{LICENSE,license,License}*'`
- `outputType`
    - Output type: `'banner'` or `'html'`
        - `'banner'`: Append comment to top of bundled code
        - `'html'`: Generate html (e.g. `license.[name].html`)
    - Default: `'banner'`
- `includeLicenseFile`
    - Include and put LICENSE file
    - Default: `true`

# LICENSE

MIT
