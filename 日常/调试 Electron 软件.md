
1. 打开控制台，一般是按 `option + command + i`
2. 如果不想打开，那么就配置 `globalShortcut.isRegistered`
```js
globalShortcut.register('Option+Command+I', () => { // 什么都不做，阻止默认行为 });
```

> https://www.electronjs.org/docs/latest/api/global-shortcut

3. 如果想在设置了禁止打开控制台的 electron 软件中，想打开控制台调试，那么需要使用 chrome 浏览器。

**先确保 Discord 完全关闭**，从活动监视器中看，没有任何 discord 的后台服务运行。
**通过命令行启动 Discord**：

```shell
open -n /Applications/Discord.app --args --remote-debugging-port=9222
```
**使用 Chrome 进行远程调试**：
- chrome://inspect
- 在 “Remote Target” 部分，你应该能看到 Discord 进程。点击 “inspect” 链接以打开开发者工具。
