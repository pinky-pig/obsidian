**`plugins`是一个插件，里面自己定义的规则（写法规则）和处理器（处理不同类型的文件）。**

> [Eslint 官方中文文档 - 创建插件](https://zh-hans.eslint.org/docs/latest/extend/plugins#%E6%8F%92%E4%BB%B6%E5%91%BD%E5%90%8D)

## 自定义 Rules 和自定 Fix

官方推荐使用 [Yeoman 生成器](https://www.npmjs.com/package/generator-eslint) 来创建插件。

```bash
npm i -g yo
npm i -g generator-eslint
yo eslint:plugin
yo eslint:rule
```

## 开发 Rules 插件
