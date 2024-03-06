
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