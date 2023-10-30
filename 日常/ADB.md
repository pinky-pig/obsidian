
> 电脑上安装 ADB ，用来调试安卓手机。下载 Android Studio 然后再安装 ADB 并且配置环境变量。

## 电脑运行Python脚本控制手机

- **连接手机：** 老生常谈，开发者模式和 USB 调试,
- **开启 ADB：** `adb start-server` 
- **验证连接：** `adb devices` 查看设备 ID
- **安装 Python：** <https://www.python.org/> 并配置环境变量。然后
- **运行命令：** 在控制台输入 `python` 进入 python 环境。执行 python 命令。

```python
import os
# adb shell input keyevent 26 是触发电源键（息屏或者锁屏） 。
os.system("adb shell input keyevent 26")
```


## 手机端运行Python脚本

> Termux 是一款在 Android 设备上模拟 Linux 环境的终端模拟器和 Linux 发行版。它允许你在 Android 手机上运行 Linux 命令和应用程序，包括 Python 和其他编程语言。

- **下载 Termux：**
- - [Termux GitHub](https://github.com/termux/termux-app) 
- - [Termux 下载地址](https://f-droid.org/en/packages/com.termux/) 
- **安装 Python：** `apt install python`
- **更新软件包**：** `apt update`
- 
