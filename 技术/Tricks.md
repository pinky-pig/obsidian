
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

```
const scale = ['scaleX(1)', 'scaleX(-1)']
const animation = domRef.current.animate(
  { transform: to === 'music' ? scale : [...scale].reverse() },
  { duration: 400, fill: 'forwards' },
)
animation.onfinish = () => { }
```

```
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