**`plugins`是一个插件，里面自己定义的规则（写法规则）和处理器（处理不同类型的文件）等等。**

> [Eslint 官方中文文档 - 创建插件](https://zh-hans.eslint.org/docs/latest/extend/plugins#%E6%8F%92%E4%BB%B6%E5%91%BD%E5%90%8D)

下面创建最基础简单的规则作为样例。

## 🌸自定义 Rules 

> [Yeoman 生成器](https://www.npmjs.com/package/generator-eslint) - 官方推荐使用的创建器

#### 1.安装脚手架依赖
```bash
npm i -g yo
npm i -g generator-eslint
yo eslint:plugin
yo eslint:rule
```

#### 2.创建插件包文件夹
```bash
mkdir eslint-config
cd eslint-config
```
#### 3.使用脚手架创建 Plugin 和 Rule 

```bash
# 创建插件，会填一些配置项
yo eslint:plugin
# 创建规则，也会填一些配置项
yo eslint:rule
```

##### 使用 `yo eslint:plugin` 创建插件:
![[Pasted image 20240327153535.png]]

a. 使用 `VsCode` 打开文件夹
```bash
code .
```

b. 打开 `package.json` 更改一下 `name` 和 `description`
```json
{
  "name": "@arvin/eslint-config",
  "version": "0.0.0",
  "description": "arvin's eslint-config"
}
```

c. 文件目录介绍
- `lib/rules` 文件夹下写规则
- `lib/index.js` 规则导出及配置项
- `tests/lib/rules` 文件夹下写测试

##### 使用 `yo eslint:rule` 创建插件:
![[Pasted image 20240327155110.png]]

a. 生成的文件目录
![[Pasted image 20240327155353.png]]

b. 打开要开发的规则文件代码看看

发现报红色提示
```
`meta.messages` must contain at least one violation message.eslint[eslint-plugin/prefer-message-ids](https://github.com/eslint-community/eslint-plugin-eslint-plugin/tree/HEAD/docs/rules/prefer-message-ids.md)
```
其实就是缺少 `message` 提示，到打开*提示*的链接，到官网拷贝代码过来就好了。

c. 开始编写测试用例代码
```js
/**
 * @fileoverview 不许使用 alert
 * @author arvin
 */
"use strict";

//------------
// 引入规则
//------------
const rule = require("../../../lib/rules/no-alert"),
  RuleTester = require("eslint").RuleTester;


//------------------------------------------------------------------------------
// 测试
//------------------------------------------------------------------------------

const ruleTester = new RuleTester();

//------------
// 引入提示信息，就是上一步引入的。这里其实随便写都可以，只要最后能过测试用例！
//------------
const [ MESSAGE_ID_DEFAULT ] = Object.keys(rule.meta.messages);

ruleTester.run("no-alert", rule, {
  valid: [ ],
  invalid: [
    {
      code: "alert(0)",
      errors: [{ messageId: MESSAGE_ID_DEFAULT }],
    },
  ],
});
```

d. 准备编写规则 Rule 代码
测试用例已经写了一个，`alert(0)`是报错的，接下来就是要在 Rule 代码中实现。

![[Pasted image 20240327160553.png]]

由上面AST分析器可知，alert会在这里触发。于是开始**调试代码**。其实在使用脚手架创建项目的时候，已经安装了调试代码的依赖，就是 `mocha` 这个包。

###### 调试代码
1. Vscode 进入调试 JS 模式
2. 打断点
3. 运行命令调试
