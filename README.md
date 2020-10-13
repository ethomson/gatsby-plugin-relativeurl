# gatsby-plugin-relativeurl

[![NPM version][npm-image]][npm-url]

[npm-url]:https://npmjs.org/package/gatsby-plugin-relativeurl

Updates [Gatsby](https://www.gatsbyjs.org/) generated URLs to be relative, suitable for using `file:///` based paths or deploying to [IPFS](https://ipfs.io/).  This is an extension of the exceedingly clever [gatsby-plugin-ipfs](https://github.com/moxystudio/gatsby-plugin-ipfs) by [André Cruz](https://github.com/moxystudio).

This plugin adds support for literal paths, adding `index.html`, since browsers cannot handle an implicit `index.html` in `file:///` URLs that point to directories.


## Installation

```sh
$ npm install --save gatsby-plugin-relativeurl
```


## Usage

Set `prefixPath` to `__GATSBY_RELATIVEURL_PATH_PREFIX__` and include the plugin in your `gatsby-config.js` file:

```js
module.exports = {
    pathPrefix: '__GATSBY_RELATIVEURL_PATH_PREFIX__',
    plugins: [
        'gatsby-plugin-relativeurl',
    ],
};
```

And now, simply build the project with `npm run build -- --prefix-paths`. Better yet, set it by default in your `package.json`:

```json
"scripts": {
  "build": "gatsby build --prefix-paths"
},
```


## But how?

It turns out the Gatsby doesn't support relative paths. But I didn't gave up and came up with smart and ugly hacks to do so:

- Adds a very small code snippet to every HTML page that defines the `__GATSBY_RELATIVEURL_PATH_PREFIX__` global based on the browser location
- Adds a post-build step that iterates over files and transforms every `__GATSBY_RELATIVEURL_PATH_PREFIX__` occurrence


## License

[MIT License](http://opensource.org/licenses/MIT)
