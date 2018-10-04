# 指定顺序执行函数🐑

## EXPLAIN 
创建一个函数，该函数使用根据指定索引排列的参数调用所提供的函数。
```javascript
const rearg = (fn, indexes) => (...args) => fn(...indexes.map(i => args[i]));
```
## REVISE
 
## USE
使用Array.prototype.map()结合spread运算符(…)对参数进行重新排序，将转换后的参数传递给fn。
## EXAMPLES 
```javascript
const rearged = rearg(
  function(a, b, c) {
    return [a, b, c];
  },
  [2, 0, 1]
);
rearged('b', 'c', 'a');
```