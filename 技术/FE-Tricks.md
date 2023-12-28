
- IndexDB
- Broadcast Channel()
- PWA
- Worker



[JS label](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/label)


1. **++ 取余**

```
let count = 0
count = (count + 1) % 11
```

2. **mix-blend-mode: difference**
要同时设置 color 和 mix-blend-mode ，一般用于黑白

```
{
	color: white;
	mix-blend-mode: difference;
}
```


3. **PointerEvent 在移动端**

PointerEvent 事件对应的dom设置 touch-action:none

4. **动画的回调**

```js
const scale = ['scaleX(1)', 'scaleX(-1)']
const animation = domRef.current.animate(
  { transform: to === 'music' ? scale : [...scale].reverse() },
  { duration: 400, fill: 'forwards' },
)
animation.onfinish = () => { }
```

```js
const ANIMATIONS = document.getAnimations();
  console.info({ ANIMATIONS })
  await Promise.all(ANIMATIONS.map((animation) => animation.finished))
  console.info("done");
```

**5. view transition api**
> https://developer.chrome.com/docs/web-platform/view-transitions/


**6. fileURLToPath**

```ts
import { fileURLToPath } from 'node:url'
export default defineConfig({
  resolve: {
    alias: {
      '@eslint-stylistic/metadata': fileURLToPath(new URL('../../packages/metadata/src/index.ts', import.meta.url)),
    },
  },
 }
```

**7.  Nodejs 下载文件**

```js
const axios = require('axios');
const fs = require('fs');
const path = require('path');

const urls = Array(11).fill(0).map((_, i) => {
  return `http://192.168.50.35:19090/fcscloud/view/preview/90jbNTZ8er-FoT8DLA4wS51rBC94o58XnIy_gDOtu_K3foWjAdE0jhpky4TN-kks5ValZz-ghoqBBQQik4kR9siVANZdfZT2Pbdq6TI5ntYa76AyxjsO5Mkr2yuYgpPDkfoDTr4dRP4S-oyGRmhPmDC6X375g5thUS0S0APrN1J5-dE7WWSxXwg8H11noZ1yjACqx2FdQNjsLkOuGggObQt9vrfy4AfyiGruMF4cqj08diHx5g7CP-PhJtvK9Lq_xcy3CIG5AVz_hu5YAAFmB_Gxawj6HwRJ03nGgbuAfOGmo5fCM5L77cTjdsdcGPQ_FU2h6K4Gdj2jkEw3i5ucMIZAKdfabHY9ItTq059eHQM4FJuH7QOT871j4XYr_ibeUwV3v0etAyOeuXExC8-Nn7hBi4SLldY0SOSNn980StJ9ijDPWNLXJarDEcqdCDetu14qgW4h3W2rgGuWHK4nrAECVxIkEZghXM3L54l7eg8VTig3jchLcMUhpXiJp5oGrkDBOLx-VcfkKd8eJSNW39AFsd6NxHrhyk4XXY6U6Oa-034A1Gm7ps0L1VldnSPZC8QxuhI5hEVWuA4p2mjYNOxW4eWBHoR3xG676LeddWx0fQRESqgN0S34BL3OmMKn7TcmZoK2VilV3LEwtCLOcZwVOOfhU7-qugOxAS_E2qXr5VT5F7yhz9GJhZ3pCEJcx4h0-roEqZSAV8E-LrZUpVzHgw-XZmDseJ8n9yM2Otc5Luab0dFivKXblwy7cEJULyioa8eXI-ueaYusHphyLbYKV6dYR40bBn1gRD6xH5uTA0HdFrVwRkuESwsPvNgbOk5A9Q5-deuaweYmIt79MSpF55POFpOZkr5FSFqrcd30J1mCCmJ5X6CdLygniwRB1V6r2rBhUOtt5RqTRD2tWrzMfC7qheNb7Ilowz_yF3tB6Jq83_ZWULb-BsC3dujCSU12nnEjeAgcoQqYk9QzHQ==/${i}.svg?t=0.6394264746619498`
});

const outputFolder = '/path/to/your/local/folder'; // 保存文件的本地文件夹

async function downloadFile(url, outputPath) {
  const response = await axios({
    method: 'get',
    url: url,
    responseType: 'stream',
  });

  const writer = fs.createWriteStream(outputPath);

  response.data.pipe(writer);

  return new Promise((resolve, reject) => {
    writer.on('finish', resolve);
    writer.on('error', reject);
  });
}

async function downloadAllFiles() {
  for (let i = 0; i < urls.length; i++) {
    const outputPath = path.join(outputFolder, `file${i}.svg`);
    await downloadFile(urls[i], outputPath);
    console.log('File downloaded to', outputPath);
  }
}

downloadAllFiles();


```

**8.  CloneNode 克隆 DOM 节点**

> https://developer.mozilla.org/en-US/docs/Web/API/Node/cloneNode

```js
let p = document.getElementById("para1");
let p_prime = p.cloneNode(true);
```


**9.  拷贝节点样式**

```js
const phElement = document.createElement('div')
const computedStyles = getComputedStyle(ele as HTMLElement)
for (let i = 0; i < computedStyles.length; i++) {
	const property = computedStyles[i]
	const value = computedStyles.getPropertyValue(property)
	phElement.style.setProperty(property, value)
}
```

**10.  默认样式**

```css

/* 滚动条 */
::-webkit-scrollbar{
  width:6px;
  height:6px;
  background-color: transparent;
  border-radius: 8px;
}

::-webkit-scrollbar-track-piece{
  width:24px;
  background-color:transparent;
  border-radius: 8px;
}

::-webkit-scrollbar-thumb:vertical{
  width:24px;
  height:24px;
  background: rgb(214, 212, 212);
  border-radius: 8px;
}

::-webkit-scrollbar-thumb:horizontal{
  width:24px;
  height:24px;
  background: rgb(214, 212, 212);
  border-radius: 8px;
}

::-webkit-scrollbar-button{
  display:none;
}

::-webkit-scrollbar-corner{
  display:none;
}


/* 文字选中颜色 */
::selection {
  background-color: #fff;
  color: #000;
}
```


**11.  获取一个 DOM 在页面中的绝对位置**

|API|用途|文档|标准|
|---|---|---|---|
|`offsetTop`|相对定位容器的位置|[MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetTop)|[CSSOM View Module](https://drafts.csswg.org/cssom-view/#dom-htmlelement-offsettop)|
|`clientTop`|上边框宽度|[MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/clientTop)|[CSSOM View Module](https://drafts.csswg.org/cssom-view/#dom-element-clienttop)|
|`.getBoundingClientRect()`|元素大小和相对视口的位置|[MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect)|[CSSOM View Module](https://drafts.csswg.org/cssom-view/#dom-element-getboundingclientrect)|
|`.getClientRects()`|所有子 CSS 盒子的大小和位置|[MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/getClientRects)|[CSSOM View Module](https://drafts.csswg.org/cssom-view/#dom-element-getclientrects)|
|`.getComputedStyle()`|应用所有样式表和计算之后的 CSS 属性|[MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window/getComputedStyle)|[DOM Level 2 Style](https://www.w3.org/TR/2000/REC-DOM-Level-2-Style-20001113/css.html#CSS-CSSview-getComputedStyle) [CSSOM](https://drafts.csswg.org/cssom/#dom-window-getcomputedstyle)|

**12.  点击盒子，触发事件**

点击子元素肯定会触发父盒子的事件，要想不触发，给**子元素**添加上一个阻止冒泡就行了。

```js
e.preventDefault() 
e.stopPropagation()
```

```vue
<div @click="handleClose">
	<div @click.stop></div>
</div>
```

**12.  媒体查询**

```css
@media screen and (max-width: 710px) {
  .modal-content-container{
    flex-direction: column;
    min-width: 260px;
    width: 260px;
    margin-top: unset;
  }
}
```

**13.  一个数组根据另一个数组进行排序**

```js
const domIdArr = Array.from(currentDoms).map(item => item.id)
elementsBox.value.sort((a: any, b: any) => {
    return domIdArr.indexOf(a.id) - domIdArr.indexOf(b.id)
})
```

**14.  Draggable 拖拽**

```
- dragstart 在元素开始被拖动时触发
- dragend 在拖动操作完成时触发
- drag 在元素被拖动时触发 **四个**是用于**释放区域**的
- dragenter 当被拖动元素进入到释放区所占据的屏幕空间时触发
- dragover 当被拖动元素在释放区内移动时触发
- dragleave 当被拖动元素没有放下就离开释放区时触发
- drop 当被拖动元素在释放区里放下时触发
```