
**1. 压缩图片**

a. 下面的命令将会把 input.jpg 这张图片压缩成宽度为 640 像素，而高度会被自动计算的大小，然后保存为 output.jpg。

```bash
ffmpeg -i input.jpg -vf scale=640:-1 output.jpg
```

b. 使用 -quality 选项来控制压缩质量，除了以上的条件外，使用 80% 的质量进行压缩

```bash
ffmpeg -i input.jpg -vf scale=640:-1 -quality 80 output.jpg
```

c. 只使用质量压缩

```bash
ffmpeg -i input.jpg -quality 80 output.jpg
```

**2.批量压缩**

`win` 

a.  新建文本文档
b.  编辑写入内容如下

```bash
for %%F in (*.jpg) do ffmpeg -i "%%F" -q:v 10 "outputs\%%F"
```


```bash
for %%F in (*.jpg) do ffmpeg -i "%%F" -vf scale=640:-1 -quality 80 "outputs\%%F"
```

c. 重命名为 `xx.bat` ,双击运行

**2.压缩视频**


**a. 指定比特率**

```bash
ffmpeg -i input.mp4 -b:v 500k output.mp4
```

**b. 使用CRF（Constant Rate Factor）**

```bash
ffmpeg -i input.mp4 -crf 23 output.mp4
```

**c. 调整分辨率**

```bash
ffmpeg -i input.mp4 -vf scale=640:480 output.mp4
```

**d. 选择编码器**

```bash
ffmpeg -i input.mp4 -c:v libx265 output.mp4
```

**e. 删除音频流**

```bash
ffmpeg -i input.mp4 -an output.mp4
```


**f. 设定帧率**

```bash
ffmpeg -i input.mp4 -r 30 output.mp4
```


**3. 将 m4a 的音乐文件转为 mp4 格式**

```
ffmpeg -i input.m4a -acodec libmp3lame -q:a 2 output.mp3
```


**4. python 脚本遍历转换**

- 先找到要遍历转换的文件目录
- 创建一个文件`bat.py`
- 编辑 .py 文件，写入如下的内容
- 打开 cmd ，假如文件路径为 `D:\Mine\白噪音小程序\audio\城市` ，那么`cd D:\Mine\白噪音小程序\audio\城市`
- 然后 `python bat.py` ，即可运行 python 脚本

```
import os
import subprocess

input_folder = r'D:\Mine\白噪音小程序\audio\城市'
output_folder = os.path.join(input_folder, 'outputs')

# 创建输出文件夹（如果不存在）
os.makedirs(output_folder, exist_ok=True)

# 遍历输入文件夹中的所有 M4A 文件
for filename in os.listdir(input_folder):
    if filename.endswith('.m4a'):
        input_file_path = os.path.join(input_folder, filename)
        output_file_path = os.path.join(output_folder, os.path.splitext(filename)[0] + '.mp3')

        # 使用 subprocess 调用 FFmpeg 进行转换
        command = f'ffmpeg -i "{input_file_path}" -acodec libmp3lame -q:a 2 "{output_file_path}"'
        subprocess.call(command, shell=True)

print('Conversion completed.')

```