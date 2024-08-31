## 使用命令设置代理

你可以使用`npm config set`命令来设置HTTP和HTTPS代理。这会将代理设置保存在全局NPM配置文件中（通常位于用户[主目录](https://zhida.zhihu.com/search?q=%E4%B8%BB%E7%9B%AE%E5%BD%95&zhida_source=entity&is_preview=1)的`.npmrc`文件中）。

打开终端或[命令行界面](https://zhida.zhihu.com/search?q=%E5%91%BD%E4%BB%A4%E8%A1%8C%E7%95%8C%E9%9D%A2&zhida_source=entity&is_preview=1)，输入以下命令

```bash
npm config set proxy http://127.0.0.1:7890
npm config set https-proxy http://127.0.0.1:7890
```

这里假设你的[代理服务器](https://zhida.zhihu.com/search?q=%E4%BB%A3%E7%90%86%E6%9C%8D%E5%8A%A1%E5%99%A8&zhida_source=entity&is_preview=1)地址是`http://127.0.0.1:7890`，你需要根据你的实际代理服务器地址进行替换。

## 直接编辑`.npmrc`文件设置代理

你还可以手动编辑或创建一个`.npmrc`文件来[指定代理](https://zhida.zhihu.com/search?q=%E6%8C%87%E5%AE%9A%E4%BB%A3%E7%90%86&zhida_source=entity&is_preview=1)设置。`.npmrc`文件通常位于用户的主目录下。

打开或创建`.npmrc`文件。

添加以下行来设置代理

```text
proxy=http://127.0.0.1:7890
https-proxy=http://127.0.0.1:7890
```

保存并关闭文件。

### 清除代理设置

如果你想清除已设置的代理，可以使用以下命令

```text
npm config delete proxy
npm config delete https-proxy
```

### 验证代理设置

设置完代理后，你可以使用以下命令来检查设置是否正确

```text
npm config get proxy
npm config get https-proxy
```

这将显示当前设置的HTTP和HTTPS代理地址。