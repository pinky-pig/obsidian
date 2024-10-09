1. windows 安装 wsl

比较简单，直接参考官网。

> https://learn.microsoft.com/en-us/windows/wsl/install

命令台直接输入如下：

```bash
wsl --install
```

2. `wsl --version` 查看版本，我们使用 wsl2，最新的
3. 进入系统，会默认先设置用户名密码。这里设置为 root123/root123
4. 查看网络是否通

```
curl http://www.baidu.com
```

或者直接 ping 也可以

```
ping baidu.com
```

`curl`，全称为CommandLine URL命令行 url， https://curl.se/

5. 更新系统

```bash
sudo apt update && sudo apt upgrade
```

6. wsl 网络代理
如果提示 `wsl: 检测到 localhost 代理配置,但未镜像到 WSL。NAT 模式下的 WSL 不支持 local` ，因为 windows 开了 clash。

解决方法：


在你的windows的C:\Users\<your_username>目录下面创建一个.wslconfig文件，往里面写入下面代码

```
[experimental]
autoMemoryReclaim=gradual  
networkingMode=mirrored
dnsTunneling=true
firewall=true
autoProxy=true
```

然后关闭 wsl ，重启。

```bash
wsl --shutdown
```

再试一下：

```bash
curl https://www.google.com/
```

7. 安装 nvm

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash
```

安装完成之后，重新启动 wsl 窗口，输入命令查看 nvm 版本

```bash
nvm -v
```

8. 安装 node

先查看线上可用的版本

```bash
nvm ls-remote
```

安装一个版本的 node

```bash
nvm install v20.18.0
```

查看版本

```bash
# nvm 下载的 node 列表
nvm ls

# node 版本
node -v

# npm 版本
npm -v
```