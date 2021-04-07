# Updating `babel-eslint` to `@babel/eslint-parser` for React apps

As of March 2020, `babel-eslint` has been deprecated, and is now `@babel/eslint-parser`.  That doesn't stop it (as of March 2020) being downloaded *6.5 million times per week*.  You wouldn't know this unless you attempted to add it as a new dependency, in which case `yarn` would tell you:

```
warning babel-eslint@10.1.0: babel-eslint is now @babel/eslint-parser. This package will no longer receive updates.
```

You're still fine to keep linting (it won't raise any errors), though at some point you (or some dependency) will want that upgrade.  I couldn't find any useful guides for this upgrade, so assuming you're using React and a fairly standard setup (I've tested with create-react-app, nextjs, and vitejs - though I imagine the steps are similar if not identical for other setups) then the below will get you pugrad

Upgrading is straightforward but I couldn't find any clear guides - so if you want to avoid the trial and error you can follow the below steps (which I've tested on create-react-app, nextjs, and vitejs apps - which all use babel under the hood).

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

**TODO**
- for testing, installed at C:\temp\site-test -
**TODO**

[babel-eslint repo]: https://github.com/babel/babel-eslint
