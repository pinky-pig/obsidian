
```json
// manifest.json
{
  "name": "Arvin chrome theme",
  "version": "1.0",
  "manifest_version": 3,
  "description": "",
  "theme": {
    // "images": {
    //   // 用于定义浏览器窗口的框架图像。
    //   "theme_frame": "images/theme_frame.png",
    //   // 用于定义浏览器工具栏的图像。
    //   "theme_toolbar": "images/theme_toolbar.png",
    //   // 用于定义标签页背景的图像。
    //   "theme_tab_background": "images/theme_tab_background.png",
    //   // 用于定义新标签页背景的图像。
    //   "theme_ntp_background": "images/theme_ntp_background.jpeg"
    // },
    "colors": {
      // 定义浏览器窗口框架的颜色。
      "frame": [3, 6, 20],
      // 定义浏览器工具栏的颜色。
      "toolbar": [37, 40, 53],
      // 定义标签页文本的颜色。
      "tab_text": [255, 255, 255],
      // 定义标签页背景文本的颜色。
      "tab_background_text": [255, 255, 255],
      // 定义书签文本的颜色。
      "bookmark_text": [255, 255, 255],
      // 定义新标签页背景的颜色。
      "ntp_background": [255, 255, 255],
      // 定义新标签页文本的颜色。
      "ntp_text": [50, 50, 50],
      // 定义新标签页链接的颜色。
      "ntp_link": [6, 55, 116],
      // 定义按钮背景的颜色。
      "button_background": [0, 0, 0, 0]
    },

    "tints": {
      // 定义按钮颜色的变化。
      "buttons": [0.19, 0.5, 0.98]
    },

    "properties": {
      // 定义新标签页背景的对齐方式。
      "ntp_background_alignment": "top",
      // 定义新标签页背景的重复方式。
      "ntp_background_repeat": "no-repeat"
    }
  }
}
```