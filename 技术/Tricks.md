
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

5. **view transition api**
> https://developer.chrome.com/docs/web-platform/view-transitions/


6. fileURLToPath

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