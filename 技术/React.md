> vue 和 react 简单对比学习： https://juejin.cn/post/7268844150233219107?searchId=20231007114618F911C66A3C3F1217B19F
> 




1. useState 和 useReducer

> useReducer 是一个一般化的 useState，比 useState 多了一个处理函数，该函数可以根据不同的分发状态来相应的改变状态。可以这么理解，useReducer 是一个提前写好了怎么处理 state 的函数的 useState。

2. useEffect

```tsx
useEffect(() => {
    init();
}, []); // 传递空的依赖数组以确保只在组件挂载时运行一次。因为依赖的没有，所以只运行一次
```
