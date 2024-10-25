
1. 安装
```bash
npm install -g local-ssl-proxy
```

2. 找到已经启动的服务，比如在一个 vue 项目中，npm run dev 启动了，访问地址是： http://localhost:3000
3. 开始代理
```bash
# 这里的 9000 就是后面的 https 的端口
local-ssl-proxy --source 9000 --target 3000
```
4. 访问
```
https://localhost:9000
```