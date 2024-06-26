
```
PATH="$PATH":/usr/local/mysql/bin
mysql -u root -p
show databases;
/usr/local/mysql-8.4.0-macos14-arm64/support-files/mysql.server
```

如果提示这个
> mac Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)

<https://www.cnblogs.com/gongyuhonglou/p/9019880.html>

```bash
sudo mysqld_safe
```
等着结果

配置环境变量启动
```shell
open -e .bash_profile
open -e  ~/.zshrc
```

写入`export PATH=${PATH}:/usr/local/mysql/bin`

```shell
source ~/.zshrc
mysql --version
mysql -u root -p
```