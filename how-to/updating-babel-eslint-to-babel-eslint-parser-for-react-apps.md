# Updating `babel-eslint` to `@babel/eslint-parser` for React apps

As of March 2020, `babel-eslint` has been deprecated, and is now `@babel/eslint-parser`.  That doesn't stop it (as of March 2021) being downloaded *6.5 million times per week*.  You wouldn't know this unless you attempted to add it as a new dependency, in which case `yarn` would tell you:

```
warning babel-eslint@10.1.0: babel-eslint is now @babel/eslint-parser. This package will no longer receive updates.
```

Upgrading is straightforward but I couldn't find any clear guides - so if you want to avoid the trial and error you can follow the below steps (which I've tested on create-react-app, nextjs, and vitejs apps - which all use Babel under the hood).

As to *why* `babel-eslint` has been deprecated?  It's documented in the (now archived) [babel-eslint repo]:

> As of the v11.x.x release, babel-eslint now requires Babel as a peer dependency and expects a valid [Babel configuration file](https://babeljs.io/docs/en/configuration) to exist. This ensures that the same Babel configuration is used during both linting and compilation.

## Short version
- Remove `babel-eslint`
- Add `@babel/eslint-parser` `@babel/core` `@babel/preset-react`
- Update parser (to `@babel/eslint-parser`)
- Add the following to the `parserOptions` configuration in the `eslintrc.js` file
```js
requireConfigFile: false,
babelOptions: {
  presets: ["@babel/preset-react"]
}
```

## Longer version

First, update the parser by removing `babel-eslint` and installing `@babel/eslint-parser`:

```shell
yarn remove babel-eslint
yarn add @babel/eslint-parser -D
```

And then update the parser (in the `.eslintrc.*` file):

```javascript
  parser: '@babel/eslint-parser',
```

If you lint you'll now probably get an error about config files:

```
 0:0  error  Parsing error: No Babel config file detected for C:\temp\site-test\tailwind.config.js. Either disable config file checking with requireConfigFile: false, or configure Babel so that it can find the config files
```

To fix this we need to modify `parserOptions`:

```javascript
  parserOptions: {
    requireConfigFile: false,
  },
```

And now if we lint?  An error around React, which helpfully tells us how to fix the issue:

```
 18:4  error  Parsing error: C:\temp\site-test\src\templates\blog-post.js: Support for the experimental syntax 'jsx' isn't currently enabled (18:5):
  16 |
  17 |   return (
> 18 |     <Layout>
     |     ^

Add @babel/preset-react (https://git.io/JfeDR) to the 'presets' section of your Babel config to enable transformation.
If you want to leave it as-is, add @babel/plugin-syntax-jsx (https://git.io/vb4yA) to the 'plugins' section to enable parsing
```

So let's install the plugin:

```shell
yarn add @babel/preset-react -D
```

And then update our parserOptions to pass this option through to Babel:

```javascript
parserOptions: {
  requireConfigFile: false,
  babelOptions: {
    presets: ["@babel/preset-react"],
  },
},
```

And we'll finally be able to lint!

> In some cases you may get an error requiring @babel/core - if this isn't a dependency installed by any other packages you have installed then you'll need to install it, as it's a required peer dependency for both `@babel/eslint-parser` and `@babel/preset-react`.

[babel-eslint repo]: https://github.com/babel/babel-eslint
