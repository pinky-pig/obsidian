
1. 读取文件并写入
```js
const fs = require('fs')
const path = require('path')

// 获取当前文件所在的文件夹路径
const folderPath = path.join(__dirname, 'src/views/chemical/hazardous')

// 定义要写入的 txt 文件相对路径
const txtFilePath = path.join(__dirname, '/output.txt')

// 读取文件夹下的所有文件
fs.readdir(folderPath, (err, files) => {
  if (err) {
    console.error('Error reading folder:', err)
    return
  }

  // 遍历每个文件
  files.forEach((file) => {
    // 构建文件的完整路径
    const filePath = path.join(folderPath, file)

    // 读取文件内容并累加到 combinedContent 变量中
    fs.readFile(filePath, 'utf8', (err, data) => {
      if (err) {
        console.error('Error reading file:', err)
        return
      }

      const fileName = path.basename(filePath)

      const combinedContent = `${fileName}\n\n${data}\n\n`

      // 将文件内容写入到 txt 文件中
      fs.appendFile(txtFilePath, combinedContent, (err) => {
        if (err) {
          console.error('Error writing to txt file:', err)
          return
        }
        console.log(`Appended content of ${file} to ${txtFilePath}`)
      })
    })
  })
})


```