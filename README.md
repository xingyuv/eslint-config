# @xingyuv/eslint-config

[![npm](https://img.shields.io/npm/v/@xingyuv/eslint-config?color=444&label=)](https://npmjs.com/package/@xingyuv/eslint-config) [![code style](https://xingyuv.com/badge-code-style.svg)](https://github.com/xingyuv/eslint-config)

- Single quotes, no semi
- Auto fix for formatting (aimed to be used standalone **without** Prettier)
- Designed to work with TypeScript, Vue out-of-box
- Lint also for json, yaml, markdown
- Sorted imports, dangling commas
- Reasonable defaults, best practices, only one-line of config
- **Style principle**: Minimal for reading, stable for diff

## Usage

### Install

```bash
pnpm add -D eslint @xingyuv/eslint-config
```

### Config `.eslintrc`

```json
{
  "extends": "@xingyuv"
}
```

> You don't need `.eslintignore` normally as it has been provided by the preset.

### Add script for package.json

For example:

```json
{
  "scripts": {
    "lint": "eslint .",
    "lint:fix": "eslint . --fix"
  }
}
```

### VS Code support (auto fix)

Install [VS Code ESLint extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

Add the following settings to your `settings.json`:

```jsonc
{
  "prettier.enable": false,
  "editor.formatOnSave": false,

  // Auto fix
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true,
    "source.organizeImports": false
  },

  // Silent the stylistic rules in you IDE, but still auto fix them
  "eslint.rules.customizations": [
    {
      "rule": "@stylistic/*",
      "severity": "off"
    }
  ],

  // The following is optional.
  // It's better to put under project setting `.vscode/settings.json`
  // to avoid conflicts with working with different eslint configs
  // that does not support all formats.
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "typescript",
    "typescriptreact",
    "vue",
    "html",
    "markdown",
    "json",
    "jsonc",
    "yaml"
  ]
}
```

### TypeScript Aware Rules

Type aware rules are enabled when a `tsconfig.eslint.json` is found in the project root, which will introduce some stricter rules into your project. If you want to enable it while have no `tsconfig.eslint.json` in the project root, you can change tsconfig name by modifying `ESLINT_TSCONFIG` env.

```js
// .eslintrc.js
const process = require('node:process')

process.env.ESLINT_TSCONFIG = 'tsconfig.json'

module.exports = {
  extends: '@xingyuv'
}
```

### Lint Staged

If you want to apply lint and auto-fix before every commit, you can add the following to your `package.json`:

```json
{
  "simple-git-hooks": {
    "pre-commit": "pnpm lint-staged"
  },
  "lint-staged": {
    "*": "eslint --fix"
  }
}
```

and then

```bash
npm i -D lint-staged simple-git-hooks
```

## Badge

If you enjoy this code style, and would like to mention it in your project, here is the badge you can use:

```md
[![code style](https://xingyuv.com/badge-code-style.svg)](https://github.com/xingyuv/eslint-config)
```

[![code style](https://xingyuv.com/badge-code-style.svg)](https://github.com/xingyuv/eslint-config)

## FAQ

### Prettier?

[Why I don't use Prettier](https://xingyuv.me/posts/why-not-prettier)

### How to lint CSS?

This config does NOT lint CSS. I personally use [UnoCSS](https://github.com/unocss/unocss) so I don't write CSS. If you still prefer CSS, you can use [stylelint](https://stylelint.io/) for CSS linting.

### I prefer XXX...

Sure, you can override the rules in your `.eslintrc` file.

<!-- eslint-skip -->

```jsonc
{
  "extends": "@xingyuv",
  "rules": {
    // your rules...
  }
}
```

Or you can always fork this repo and make your own.

## License

[MIT](./LICENSE) License &copy; 2023-PRESENT [xingyuv](https://github.com/xingyuv)
