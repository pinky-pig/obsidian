
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


## 手机端运行Python脚本（Android 11+）

核心就是手机端装控制台，连接 ADB ，装 Python 环境，运行 Python 脚本。

> Termux 是一款在 Android 设备上模拟 Linux 环境的终端模拟器和 Linux 发行版。它允许你在 Android 手机上运行 Linux 命令和应用程序，包括 Python 和其他编程语言。  
> 需要 Android 11 + 是因为要想在手机端连接 ADB 控制手机，需要无线调试，而这是 11 以上的版本才有的。


```bash
# 设置 kill false 自动杀死后台
adb shell "settings put global settings_enable_monitor_phantom_procs false"
```


- **下载 Termux：**
- - [Termux GitHub](https://github.com/termux/termux-app) 
- - [Termux 下载地址](https://f-droid.org/en/packages/com.termux/) 
- **存储授权：** `termux-setup-storage` 弹出窗口，打开存储权限。进到根目录 `cd /sdcard/` 操作。
- **新建文件夹：** `mkdir workspace`  `cd workspace` 目的是，在电脑端调试好脚本后，直接导入到这个文件夹，再在手机端运行脚本。当然直接在手机端调试也行。这个时候，脚本的文件夹就是在根目录 `/sdcard/workspace` 。
- **安装 Python：** `pkg install python`
- **安装工具包：** `pkg install  android-tools` 这个是为了在手机端下载 ADB 。

准备连接
- **打开无线调试：** 打开手机的无线调试，然后将当前"设置"窗口分屏。
- **使用配对码配对设备：** 点击配对码，然后切换到 Termux 窗口。
- **配对：** `adb pair ip:port`  这里ip和port是配对码页面的。
- **连接：** `adb connect ip:port`  这里ip和prot是无线调试页面页面的。连接成功，无线调试页面也会有窗口信息提示。
- **检查：** `adb devices`  如果连接成功，会打印出连接配对的机子的信息。
- **执行 Python 命令：**
```python
import os

# home键
os.system("adb shell input keyevent 3")

# 屏幕上滑
os.system("adb shell input swipe 200 1800 300 1200")

# 打开钉钉
os.system("adb shell am start com.alibaba.android.rimet/.biz.LaunchHomeActivity")

# 触发点击某个像素点位置
os.system("adb shell input tap 96 1112")
```
- **执行 Python 脚本：**
```bash
cd /sdcard
cd workspace

nohup python -u auto-dd.py > log.log 2>&1 &
```
- **查看日志：**
```bash
tail -f log.log
```



## 脚本示例：自动钉钉打卡


```python
# -*- coding: utf-8 -*-

'''
@Project ：exe 
@File    ：auto.py
@IDE     ：PyCharm 
@Author  ：Sadhu
@Date    ：2023/10/26 10:10 
'''
import os
import time
import schedule
import smtplib

from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.image import MIMEImage

class Email():
    def __init__(self):
        self.__SMTP_SSL_HOST = 'smtp.163.com'
        self.__SMTP_SSL_PORT = '465'
        self.__from_email_address = '13912258252@163.com'
        self.__from_email_password = 'XMDRPORIXPBXMVTM'
        self.__to_email_address = '675887342@qq.com'

    def __link_and_login(self):
        # 1. 连接邮箱服务器
        con = smtplib.SMTP_SSL(self.__SMTP_SSL_HOST, self.__SMTP_SSL_PORT)
        # 2. 登录邮箱
        con.login(self.__from_email_address, self.__from_email_password)
        return con

    def send(self, subject, body, image_data_list=[]):
        msg = MIMEMultipart()
        msg['From'] = self.__from_email_address
        msg['To'] = self.__from_email_password
        msg['Subject'] = subject
        if len(image_data_list) > 0:
            body = body + '<br/>'
            for i, image_data in enumerate(image_data_list):
                body = body + f'<img src="cid:image{i}">'
                image = MIMEImage(image_data)
                image.add_header('Content-ID', f'<image{i}>')
                msg.attach(image)
        html = MIMEText(body, 'html')
        msg.attach(html)
        con = self.__link_and_login()
        con.sendmail(self.__from_email_address, self.__to_email_address, msg.as_string())
        print(f'邮件: {subject} 已完成发送')
        # 关闭连接
        con.quit()


email = Email()


def log():
    nowtime = time.strftime("%Y-%m-%d %H:%M:%S", time.localtime())
    print(f'程序正在运行，当前时间 {nowtime}')


def auto():
    # 电源键
    os.system("adb shell input keyevent 26")
    time.sleep(3)
    # 屏幕上滑
    os.system("adb shell input swipe 200 1800 300 1200")

    # home键
    os.system("adb shell input keyevent 3")
    # 打开钉钉
    # os.system("adb shell input tap 96 1112")
    os.system("adb shell am start com.alibaba.android.rimet/.biz.LaunchHomeActivity")
    time.sleep(10)
    # 选择工作台
    os.system("adb shell input tap 527 2140")
    # 选择打卡
    time.sleep(10)
    os.system("adb shell input tap 94 977")
    time.sleep(10)
    # 点击打卡
    os.system("adb shell input tap 525 1349")
    time.sleep(10)
    # 关闭钉钉
    os.system("adb shell am force-stop com.alibaba.android.rimet")
    # 电源键，锁屏
    os.system("adb shell input keyevent 26")
    nowtime = time.strftime("%Y-%m-%d %H:%M:%S", time.localtime())
    print(f'{nowtime} 已打卡')


if __name__ == "__main__":
    nowtime = time.strftime("%Y-%m-%d %H:%M:%S", time.localtime())
    print(f"{nowtime} 开始执行！")
    res = os.system("adb devices")
    print(res)

    schedule.every().hours.do(log)

    schedule.every().monday.at("08:45:35").do(auto)
    schedule.every().tuesday.at("08:46:25").do(auto)
    schedule.every().wednesday.at("08:44:55").do(auto)
    schedule.every().thursday.at("08:45:15").do(auto)
    schedule.every().friday.at("08:47:05").do(auto)

    schedule.every().monday.at("18:01:05").do(auto)
    schedule.every().tuesday.at("18:01:16").do(auto)
    schedule.every().wednesday.at("18:02:01").do(auto)
    schedule.every().thursday.at("18:01:07").do(auto)
    schedule.every().friday.at("18:00:59").do(auto)

    schedule.every().monday.at("20:02:11").do(auto)
    schedule.every().tuesday.at("20:01:26").do(auto)
    schedule.every().thursday.at("20:04:07").do(auto)

    while True:
        schedule.run_pending()
        time.sleep(1)
```


## 常用命令集


```python
adb shell  
```


**传输文件**

```bash
adb push "C:\Users\Admin\Desktop\test.py" "/sdcard/workspace"
```

**运行脚本**

```bash
nohup python -u auto.py
```

**adb重启或关机手机命令**

重启：

```python
adb reboot
```

若连接多台手机，可通过设备号对指定手机重启：

```python
adb -s device1 reboot
如
adb -s 112.113.114.115:5555 -s device1 reboot
```

关机：如果不方便开机，慎用！

```python
 adb shell reboot -p
```

在adb查看网络( adb shell ifconfig wlan0 )，返回ifconfig: ioctl 8927: Permission denied 解决方案：
```python
adb shell ip addr show wlan0
```

**Android adb命令唤醒屏幕或者熄屏**

```python
adb shell input keyevent 26   
```

**Android adb打开浏览器并访问网址**

```python
adb shell  
```

```python
am start -a android.intent.action.VIEW -d http://www.baidu.com
```



**1. 获取序列号:**
```python
adb get-serialno
```
**2. 查看连接计算机的设备：**
```python
adb devices
```  
**3. 重启机器：**
```python
adb reboot
```
**4. 重启到bootloader，**即刷机模式：
```python
adb reboot bootloader
```
**5. 重启到recovery，**即恢复模式：
```python
adb reboot recovery
```
**6. 查看log：**
```python
adb logcat
```
**7. 终止adb服务进程：**
```python
adb kill-server
```
**8. 重启adb服务进程：**
```python
adb start-server 
```
**9. 获取机器MAC地址：**
```python
adb shell  cat /sys/class/net/wlan0/address
```
**10. 获取CPU序列号：**文章来源地址:https://www.yii666.com/article/346154.html
```python
adb shell cat /proc/cpuinfo
```
**11. 安装APK：**
```python
adb install <apkfile> //比如：adb install baidu.apk
``` 
**12. 保留数据和缓存文件，**重新安装apk：_文章地址https://www.yii666.com/article/346154.html_
```python
adb install -r <apkfile> //比如：adb install -r baidu.apk
```
**13. 安装apk到sd卡：**
```python
adb install -s <apkfile> // 比如：adb install -s baidu.apk
```
**14. 卸载APK：**
```python
adb uninstall <package> //比如：adb uninstall com.baidu.search
```
**15. 卸载app但保留数据和缓存文件：**
```python
adb uninstall -k <package> //比如：adb uninstall -k com.baidu.search
```
**16. 启动应用：**
```python
adb shell am start -n <package_name>/.<activity_class_name> 
```
**17. 查看设备cpu和内存占用情况：**
```python
adb shell top
```
**18. 查看占用内存前6的app：**
```python
adb shell top -m 6
```
**19. 刷新一次内存信息，**然后返回：
```python
adb shell top -n 1
```
**20. 查询各进程内存使用情况：**
```python
adb shell procrank
```
**21. 杀死一个进程：**
```python
adb shell kill [pid] 
```
**22. 查看进程列表：**
```python
adb shell ps
```
**23. 查看指定进程状态：**
```python
adb shell ps -x [PID] 
```
**24. 查看后台services信息：**
```python
adb shell service list 
```
**25. 查看当前内存占用：**
```python
adb shell cat /proc/meminfo
```
**26. 查看IO内存分区：**地址:https://www.yii666.com/article/346154.html
```python
adb shell cat /proc/iomem
```
**27. 将system分区重新挂载为可读写分区：**
```python
adb remount
```
**28. 从本地复制文件到设备：**
```python
adb push <local> <remote> 
```
**29. 从设备复制文件到本地：**
```python
adb pull <remote> <local> 
```
**30. 列出目录下的文件和文件夹，**等同于dos中的dir命令：
```python
adb shell ls
```
**31. 进入文件夹，**等同于dos中的cd 命令：
```python
adb shell cd <folder> 
```
**32. 重命名文件：**
```python
adb shell rename path/oldfilename path/newfilename 
```
**33. 删除system/**avi.apk：
```python
adb shell rm /system/avi.apk
```
**34. 删除文件夹及其下面所有文件：**
```python
adb shell rm -r <folder> 
```
**35. 移动文件：**
```python
adb shell mv path/file newpath/file
```
**36. 设置文件权限：**
```python
adb shell chmod 777 /system/fonts/DroidSansFallback.ttf
```
**37. 新建文件夹：**
```python
adb shell mkdir path/foldelname
```
**38. 查看文件内容：**
```python
adb shell cat <file> 
```
**39. 查看wifi密码：**
```python
adb shell cat /data/misc/wifi/*.conf 
```
**40. 清除log缓存：**
```python
adb logcat -c
```
**41. 查看bug报告：**
```python
adb bugreport
```
**42. 获取设备名称：**
```python
adb shell cat /system/build.prop
```
**43. 查看ADB帮助：**
```python
adb help
```
**44. 跑monkey：**
```python
adb shell monkey -v -p your.package.name 500
```