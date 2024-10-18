
##### window系统

1、安装pm2（建议安装到全局）

```js
 npm install pm2 -g
```

2、安装windows自启动包

```js
npm install pm2-windows-startup -g
```

3、创建开机启动脚本文件

```js
pm2-startup install
```

4、使用pm2启动项目

```js
pm2 start 项目启动文件（最好是进入到项目启动文件同级目录）
```

5、保存pm2中的项目（最好加一个保存一个）

```js
 pm2 save
```

执行完以上操作，重启电脑查看

卸载服务

```js
pm2-service-uninstall 
```

##### linux系统

1、启动服务

```js
pm2 start 项目启动文件（最好是进入到项目启动文件同级目录）
```

2、保存当前已启动的服务

```js
 pm2 save
```

3、设置开机自启配置

```js
pm2 startup
```

4、执行pm2 startup后，得到提示，复制并执行以sudo env开头的提示，用来设置环境变量

```js
sudo env ...
```

执行完以上操作，重启电脑查看

##### pm2常用命令

pm2 的服务都有一个数字 id，你可以用 id 快速操作它。下面以编号为 0 的服务为例（当然，把 id 换为应用名也是一样的）：

```js
pm2 start                  # 启动一个服务，携带 --name 参数添加一个应用名，携带参数 --watch 将观察修改重启服务

pm2 list                    # 列出当前的服务 pm2 monit # 监视每个node进程的CPU和内存的使用情况

pm2 stop 0              # 停止服务(pm2 stop 名称或id)

pm2 stop all            # 停止所有服务进程

pm2 restart 0          # 重启服务(pm2 restart app.js)

pm2 restart all        # 重启所有进程

pm2 delete 0          # 删除服务(pm2 delete app_name|app_id)

pm2 delete all        # 删除全部服务

pm2 logs                # 查看所有服务的输出日志

pm2 logs 0             # 查看服务的输出日志
```
