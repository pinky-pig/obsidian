
**1. 在父元素上hover设置子元素样式**

*group 和 peer 写法一样，而且顺序要固定*

```html
<div class="group">
	<div class="group-hover:opacity-100">...</div>
</div>
```

**2. 给兄弟元素设置样式**

```css
<label> 
	<input type="checkbox" class="peer sr-only"> 
	<span class="h-4 w-4 bg-gray-200 peer-checked:bg-blue-500"> 
</label>
```

**3. 伪元素**

```html
<div
  before="hello world"
  class="before:content-[attr(before)] before:block ..."
></div>
```

