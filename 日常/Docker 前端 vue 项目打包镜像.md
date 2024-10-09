
# 不写命令，纯点点点，打包前端项目为 docker 镜像

os: windows
前端: vue
编辑器: vscode

**windows：**
1. 安装
直接[官网](https://www.docker.com/) 下载安装，跟安装普通软件一样。

安装好后会重启电脑，启动后终端查看版本

```bash
# 会输出：Docker version 27.2.0, build 3ab4256
docker -v
```

运行界面：

![[Pasted image 20241009173300.png]]

2. docker 设置
因为国内镜像源都挂了，所以还是用官方的吧。
拉镜像的时候，网络不佳需要设置代理。

可能需要设置代理（也可能不需要：

```bash
set http_proxy=http://127.0.0.1:7890 
set https_proxy=http://127.0.0.1:7890
```


![[Pasted image 20241009173543.png]]

如果需要设置 dns 的话，是在上图的 “Docker Engine” 中的 json 内容设置。

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

这样就可以发送给别人了