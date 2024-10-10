
# 不写命令，纯点点点，打包前端项目为 docker 镜像

os: windows
前端: vue
编辑器: vscode

**windows：**
1. 安装
直接[官网](https://docs.docker.com/desktop/release-notes/#new-6) 下载安装，跟安装普通软件一样，我没有使用最新版，使用的是 4.29.0版本的。

安装好后会重启电脑，启动后终端查看版本。

```bash
# 会输出：Docker version 27.2.0, build 3ab4256
docker -v
```

运行界面：

![[Pasted image 20241009173300.png]]

跟 wsl 一样，docker 默认也都是到 c 盘，不太合适。所以也跟上一章将 wsl 放到了 D 盘一样，这里将 docker 放到 D 盘，总体思路差不多。

主要是 docker-desktop 软件运行的时候的数据`docker_data.vhdx`比较大，默认路径会放在`C:\Users\Admin\AppData\Local\Docker\wsl\disk` 中。

3.1 首先启用这个

![[Pasted image 20241010143404.png]]

3.2 在终端输入
```bash
wsl -l -v
```

![[Pasted image 20241010150027.png]]

这里正在运行的有三个，其中两个 docker ，而其中占体积最大的就是这个 docker-desktop-data 。

3.3 先关闭服务

```bash
wsl --shutdown
```

3.4 跟之前迁移 wsl 一样的路子，先打包导出，然后取消注册，再导入打包后的

```bash
# 导出
wsl --export docker-desktop-data D:\docker-desktop-data.tar
wsl --export docker-desktop D:\docker-desktop.tar

# 取消注册
wsl --unregister docker-desktop-data
wsl --unregister docker-desktop

# 导入
wsl --import docker-desktop-data D:\wsl\docker-desktop-data D:\docker-desktop-data.tar
wsl --import docker-desktop D:\wsl\docker-desktop D:\docker-desktop.tar
```

查看一下 `D:\wsl\docker-desktop-data` 和 `D:\wsl\docker-desktop` 目录下是否有数据，应该都是 `ext4.vhdx` 。这样就是迁移到 D 盘了，docker 运行过程中产生的数据也都在这里了。

![[Pasted image 20241010152701.png]]

4. docker 设置
因为国内镜像源都挂了，所以还是用官方的吧。
拉镜像的时候，网络不佳需要设置代理。

可能需要设置代理（也可能不需要：

```bash
set http_proxy=http://127.0.0.1:7890 
set https_proxy=http://127.0.0.1:7890
```

一般开了 clash 代理后，vscode 的 docker 插件还是拉官方镜像的时候，网络不行，那就照图下设置代理：http://127.0.0.1:7890

![[Pasted image 20241009173543.png]]

接下来设置 images 的保存地址，在如下图所示的地方修改位置：

![[Pasted image 20241010115246.png]]


3. vscode 安装 docker 插件

![[Pasted image 20241009174200.png]]

4.  项目中写 Dockerfile ，就是配置文件了

```bash
# Dockerfile
FROM node:20-alpine AS build-stage

WORKDIR /app
RUN corepack enable

COPY package.json pnpm-lock.yaml ./
RUN --mount=type=cache,id=pnpm-store,target=/root/.pnpm-store \
  pnpm install --frozen-lockfile

COPY . .
RUN pnpm build

FROM nginx:stable-alpine AS production-stage

COPY --from=build-stage /app/dist /usr/share/nginx/html
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

跟着 chatgpt 很好理解。

先拉取 node 的镜像，然后拷贝一下文件，然后安装依赖，再运行打包命令。

然后拉取 nginx 的镜像，从刚才打包后的文件拷贝一下，到 nginx 镜像的那个路径下，设置端口为 80 端口。

5. 点点点生成镜像，运行镜像
![[docker-vscode.gif]]

以上就是打包好了镜像，但是如何找到这个镜像，发给另一台机子运行呢。

6. 压缩镜像 images 为  tar

第一步，获取 images 的 repository 和 tag 名称。当然可以在 vscode 的 docker 插件页面中，右键那个 images，然后 copy

![[Pasted image 20241009181524.png]]

也可以在终端输入

```bash
docker images
```

找到了名字，压缩也就是一行命令，例如下面：

```bash
# docker save <image_name>:<tag> -o <output_file>.tar
docker save zkyscreen:latest -o screen.tar
```

这样就可以发送给别人了。

# 在阿里云服务器上运行

因为在我的服务器是 centOS 7 的，部署 node接口，需要直接安装 nodejs，但是 centOS 7 会报一些基础库需要更新，比较麻烦，所以我就索性使用 docker 打个镜像上去运行了。

1. centOS 先安装一个 docker

```bash
# 更新一下
sudo yum update
sudo yum upgrade

# 安装工具包
sudo yum install -y yum-utils

# 添加阿里云的仓库
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

# 安装Docker
yum install docker-ce docker-ce-cli containerd.io

# 查看 docker 版本
docker version
# 查看 docker 运行状态
systemctl status docker

# 设置开机自启
systemctl enable docker

# 查看docker启动后运行是否正常
docker info
```


基础的指令：

```bash
systemctl start docker （开启）  
systemctl status docker （状态）  
systemctl enable docker （开机启动）  
systemctl disable docker.service （取消开机自启）
systemctl stop docker （关闭）  
systemctl restat docker (重启)
systemctl list-units --type=service （查看当前启动中服务）
systemctl list-unit-files | grep enable （查看当前所有开机启动服务）
```

3. 本地先打一个 node 接口的镜像。

```bash
# 使用官方 Node.js 镜像作为基础镜像
FROM node:20-alpine AS build-stage

# 设置工作目录
WORKDIR /app

RUN corepack enable

# 复制 package.json 和 pnpm-lock.yaml（如果有）
COPY package.json pnpm-lock.yaml ./

# 安装依赖
RUN --mount=type=cache,id=pnpm-store,target=/root/.pnpm-store \
  pnpm install --force

# 复制整个项目
COPY . .

# 构建项目
RUN pnpm build

# 暴露端口（根据你的应用 app.listen）
EXPOSE 3200

# 启动应用
CMD ["node", "dist/index.js"]
```

本地跑一下没问题，准备放到服务器上。这里的端口是 3200 ，服务器的这个端口需要暴露出来。

![[Pasted image 20241010161709.png]]

开通端口后，验证一下

```bash
telnet 47.116.13.177:3200
```

压缩镜像：
```bash
docker save expressjs:latest -o expressjs.tar
```

放到服务器的某个位置：这里放到 `/usr/share/workspace` 目录下，可以 FileZilla Client 直接上传。

查看 docker 状态
```bash
systemctl status docker
```

启动 Docker 服务（如果未运行）：

```bash
sudo systemctl start docker
```

设置 Docker 服务开机启动（可选）：

```bash
sudo systemctl enable docker
```

检查镜像：

```bash
docker images
```

加载镜像：
```bash
# 加载
docker load -i /usr/share/workspace/expressjs.tar
# 查看是否加载上去
docker images
```

运行容器：
```bash
docker run --rm -d -p 3200:3200 expressjs:latest
```

查看运行状态：
```bash
docker ps
```

ok，部署完成！

![[Pasted image 20241010160815.png]]