

```txt
node_mirror: https://npm.taobao.org/mirrors/node/ npm_mirror: https://npm.taobao.org/mirrors/npm/
```

>  windows 如果安装了 nvm 后，配置了自定义文件目录，记得要将其添加到环境变量里，否则 npm i  -g  的包会找不到

```
nvm off                     // 禁用node.js版本管理(不卸载任何东西)
nvm on                      // 启用node.js版本管理
nvm install <version>       // 安装node.js的命名 version是版本号 例如：nvm install 8.12.0
nvm uninstall <version>     // 卸载node.js是的命令，卸载指定版本的nodejs，当安装失败时卸载使用
nvm ls                      // 显示所有安装的node.js版本
nvm list available          // 显示可以安装的所有node.js的版本
nvm use <version>           // 切换到使用指定的nodejs版本
nvm v                       // 显示nvm版本
nvm install stable          // 安装最新稳定版
```

# NPM

```
npm -v                     // 查看 `npm` 当前版本
npm cache clean --force    // 清理 `npm` 缓存数据
npm install -g npm         // 更新到最新版本
npm -g install npm@6.8.0   // 更新到指定版本
npm i npm@6 -g             // 或者
```