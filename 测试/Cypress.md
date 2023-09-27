
> 直接跟着教程走 ：https://docs.cypress.io/guides/

## 第一步

了解玩 Cypress 的基本概念以及使用情况后，直接 [API 文档](https://docs.cypress.io/api/commands/as) 走起

下面这是一些常用的命令:

1. **cy.visit(url)**: 用于访问网站的URL，这是测试的起始点。
2. **cy.get(selector)**: 通过选择器获取DOM元素，以便后续对其进行操作和断言。
3. **cy.contains(text)**: 通过文本内容查找DOM元素。
4. **cy.click()**: 触发点击事件，通常用于模拟用户的点击操作。
5. **cy.type(text)**: 模拟在输入字段中键入文本。
6. **cy.clear()**: 清空输入字段中的文本。
7. **cy.submit()**: 提交表单。
8. **cy.should()**: 添加断言来验证页面上的元素状态或内容。
9. **cy.wait(time)**: 在测试中添加等待时间，用于处理异步操作。
10. **cy.intercept()**: 拦截和控制网络请求，以便模拟各种场景，如模拟网络错误或延迟。
11. **cy.route()**: 在旧版本中用于拦截网络请求，现在一般使用 `cy.intercept()`。
12. **cy.reload()**: 刷新页面。
13. **cy.viewport(width, height)**: 设置浏览器窗口的视图大小。
14. **cy.scrollTo()**: 滚动到指定的DOM元素。
15. **cy.exec()**: 在Node.js中执行系统命令。
16. **cy.fixture()**: 读取外部文件中的数据，通常用于加载测试数据。
17. **cy.getCookie()**: 获取页面的Cookie信息。
18. **cy.setCookie()**: 设置页面的Cookie信息。
19. **cy.clearCookie()**: 清除页面的Cookie信息。
20. **cy.screenshot()**: 拍摄页面的屏幕截图。
## Point

- describe 中只有 it



