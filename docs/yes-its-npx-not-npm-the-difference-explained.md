# 是的，它是 npx，不是 npm

> 原文: [Yes, it’s npx, not npm — the difference explained](https://medium.com/javascript-in-plain-english/yes-its-npx-not-npm-the-difference-explained-58cbb202ec33)


当我最近开始学习 React 的时，看到包括我在内的很多人当看到 `npx` 而不是 `npm` 时很困混。

一些人看的了感觉很奇怪，但也没想太多。另一些人认为可能是拼写错误了，就用 npm 而不是 npx 直接运行。

当我看到这种事情发生了很多次后，我觉得值得写篇文章来说道说道。

> 它不是拼写错误，它是 npx，不是 npm ！:)

···

## NPM

众所周知，npm 就是 Node.js 包管理器，它的职责就是**包管理**和处理它们的**依赖**关系。

我们可以在 `package.json` 文件中指定项目中的所有依赖（包），这样所有人随时都能通过 `npm install` 命令来安装所有的依赖。

它也提供了`版本控制`，例如：可以为项目指定特定版本的依赖，这样可以避免因为版本升级对我们项目造成意料之外的风险。

## NPX

**[npx](https://www.npmjs.com/package/npx)** 是用来 **执行 Node 包的工具** 并在 *npm5.2* 版本与 npm 捆绑在一起。

npx 能做什么？

1. 默认情况下，它先去检查包是否存在（会在本地项目的 `node_modules/.bin` 和环境变量 `$PATH`寻找）
2. 如果存在，执行它
3. 如果不存在，则会先安装（临时）再运行。

以上列出的是它的默认行为，当然可以通过参数来阻止。

例如：运行 `npx some-package --no-install` 是就告诉 **npx** 只运行 `some-packag` 包，如果不存在也不要安装。

更多的 **npx** 参数在[这里查看](https://www.npmjs.com/package/npx)。

## 例子

如果我们有一个包名 `my-package`，我们想运行它。

如果不用 **npx**，要运行一个包就要通过包的路径来执行。

`./node_modules/bin/my-package`

或者在 `package.json` 的 `scripts` 里编写脚本。

```json
{
  "name": "something",
  "version": "1.0.0",
  "scripts": {
    "my-package": "./node_modules/bin/my-package"
  }
}
```

然后通过 `npm run my-package` 命令运行。

现在通过 **npx** 只需 `npx my-package` 命令就能轻松运行。

## 结论

`npx != npm`
