
**1. 在父元素上hover设置子元素样式**

```html
<div class="group">...</div>
<div class="group-hover-opacity-100">...</div>
```

**2. 在子元素上设置父元素样式**

```
```

**3. 伪元素**

```html
<div
  before="hello world"
  class="before:content-[attr(before)] before:block ..."
></div>
```

