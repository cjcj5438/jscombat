# 所有的函数执行args

## EXPLAIN
不是很难理解. 就不详细说了了
 ```javascript
const over = (...fns) => (...args) => fns.map(fn => fn.apply(null, args));
```
## USE

## EXAMPLES
```javascript
const minMax = over(Math.min, Math.max);
minMax(1, 2, 3, 4, 5); // [1,5]
```