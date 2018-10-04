# 管道异步函数

## EXPLAIN
为异步函数执行从左到右的函数组合。

## REVISE
> reduce数组api

    array.reduce(function(total, currentValue, currentIndex, arr), initialValue)
    total	必需。初始值, 或者计算结束后的返回值。
    currentValue	必需。当前元素
    currentIndex	可选。当前元素的索引
    arr	可选。当前元素所属的数组对象。

```javascript
// 注意每次()=> 为参数的时候 要明白里面的返回值才是参数 不认语义就无法读通
const pipeAsyncFunctions = (...fns) =>
    arg =>
        fns.reduce((p, f) =>
            p.then(f),
            Promise.resolve(arg));
```
## USE
使用spread操作符(…)使用Array.prototype.reduce()执行从左到右的函数组合。这些函数可以返回以下组合:简单值、承诺值，或者它们可以定义为通过wait返回的异步值。所有函数都必须是一元函数。

## EXAMPLES
```javascript
const sum = pipeAsyncFunctions(
    x => x + 1,
    x => new Promise(resolve => setTimeout(() => resolve(x + 2), 1000)),
    x => x + 3,
    async x => (await x) + 4
);
(async () => {
    console.log(await sum(5)); // 15 (after one second)
})();
```