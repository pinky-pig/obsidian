1. 过滤获取DOM节点
```js
const list = Array.from(document.querySelectorAll('.trans_top-wrap')).map(item => {
    return item.children[0].href
})
console.log(list)
```