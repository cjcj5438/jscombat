# ary

## explain ##

创建一个函数，该函数最多接受n个参数，而忽略任何其他参数。使用Array.prototype.slice(0,n)和spread操作符(…)调用提供的函数fn，最多调用n个参数。

```javascript
const ary=(fn,n)=>(...args)=>fn(...args.slice(0,n))
```

## use ##
比如函数有很多参数. 但是我们只想用前面几个参数时
```javascript
// 只选择前面的两个参数
const firstTwoMax = ary(Math.max, 2);
// 这了实现是截取了[2,6] [8,4],[10,undefined] 参数进行参数运算
let arr=[[2, 6, 'a'], [8, 4, 16], [10]].map(x => firstTwoMax(...x)); // [6, 8, 10]
console.log(arr)
```