# @antfu/eslint-config

[![npm](https://img.shields.io/npm/v/@antfu/eslint-config?color=a1b858&label=)](https://npmjs.com/package/@antfu/eslint-config)

- 单引号，无分号
- 自动修复格式（目标是单独使用，无需Prettier）
- 设计为与TypeScript，Vue开箱即用
- 也对json，yaml，markdown进行Lint检查
- 排序的导入，悬挂的逗号
- 合理的默认设置，最佳实践，只需一行配置
- **样式原则**：最小化阅读，稳定的差异（注：这里的"稳定的差异"可能指的是代码改动在版本控制系统如git中产生的差异清晰易读，利于代码审查和版本比较）

## Usage

### Install

```bash
pnpm add -D eslint @antfu/eslint-config
```

### Config `.eslintrc`

```json
{
  "extends": "@antfu"
}
```

> 通常情况下，你不需要`.eslintignore`文件，因为预设已经提供了它。
>
> 这里的意思是，你所使用的ESLint预设（即之前提到的`extends: ['@antfu']`）可能已经内置了一个默认的`.eslintignore`配置。`.eslintignore`文件用于告诉ESLint忽略哪些文件或目录，不进行lint检查。因此，如果预设已经提供了合理的忽略规则，你可能就不需要自己再手动创建和管理这个文件了。

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

### Config VS Code auto fix

Install [VS Code ESLint extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) and create `.vscode/settings.json`

```json
{
  "prettier.enable": false,
  "editor.formatOnSave": false,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
```

### TypeScript Aware Rules

当在项目根目录中发现`tsconfig.eslint.json`文件时，将启用类型感知规则，这将在你的项目中引入一些更严格的规则。如果你想启用它，但项目根目录中没有`tsconfig.eslint.json`文件，你可以通过修改`ESLINT_TSCONFIG`环境变量来更改tsconfig的名称。

```js
// .eslintrc.js
process.env.ESLINT_TSCONFIG = 'tsconfig.json'

module.exports = {
  extends: '@antfu'
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

## FAQ

### Prettier?

[Why I don't use Prettier](https://antfu.me/posts/why-not-prettier)

### How to lint CSS?

This config does NOT lint CSS. I personally use [UnoCSS](https://github.com/unocss/unocss) so I don't write CSS. If you still prefer CSS, you can use [stylelint](https://stylelint.io/) for CSS linting.

### I prefer XXX...

Sure, you can override the rules in your `.eslintrc` file.

<!-- eslint-skip -->

```jsonc
{
  "extends": "@antfu",
  "rules": {
    // your rules...
  }
}
```

Or you can always fork this repo and make your own.

## Check Also

- [antfu/dotfiles](https://github.com/antfu/dotfiles) - My dotfiles
- [antfu/vscode-settings](https://github.com/antfu/vscode-settings) - My VS Code settings
- [antfu/ts-starter](https://github.com/antfu/ts-starter) - My starter template for TypeScript library
- [antfu/vitesse](https://github.com/antfu/vitesse) - My starter template for Vue & Vite app

## License

[MIT](./LICENSE) License &copy; 2019-PRESENT [Anthony Fu](https://github.com/antfu)
