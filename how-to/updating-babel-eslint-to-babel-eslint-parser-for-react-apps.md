# Updating `babel-eslint` to `@babel/eslint-parser` for React apps

## Short version
- Remove babel-eslint
- Add @babel/eslint-parser @babel/core @babel/preset-react
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

As to why?  It's documented in the (now archived) babel-eslint repo (https://github.com/babel/babel-eslint):

> As of the v11.x.x release, babel-eslint now requires Babel as a peer dependency and expects a valid [Babel configuration file](https://babeljs.io/docs/en/configuration) to exist. This ensures that the same Babel configuration is used during both linting and compilation.
