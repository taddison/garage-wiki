# Updating `babel-eslint` to `@babel/eslint-parser` for React apps

If you add `babel-eslint` as a dependency you'll be told:

```
warning babel-eslint@10.1.0: babel-eslint is now @babel/eslint-parser. This package will no longer receive updates.
```

Upgrading is straightforward but the documentation isn't clear.  If you're not directly using babel (and instead are relying on something like create react app, nextjs, vitejs) the below instructions will get you back on the upgrade train and in about the same state that you started with.

> If you are using babel directly then the below will probably work but I've not tested it - you can probably drop the `requireConfigFile: false` setting.

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

As to why?  It's documented in the (now archived) babel-eslint repo (https://github.com/babel/babel-eslint):

> As of the v11.x.x release, babel-eslint now requires Babel as a peer dependency and expects a valid [Babel configuration file](https://babeljs.io/docs/en/configuration) to exist. This ensures that the same Babel configuration is used during both linting and compilation.
