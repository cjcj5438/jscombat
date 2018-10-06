# 自定义bool函数来给数组分组

## EXPLAIN 
根据谓词函数将值分成两组，谓词函数指定输入集合中的元素属于哪个组。。如果filter中的元素是真实的，集合中的相应元素属于第一组;否则，它属于第二组。
```javascript
const bifurcateBy = (arr, fn) =>
  arr.reduce((acc, val, i) => (acc[fn(val, i) ? 0 : 1].push(val), acc), [[], []]);
```
## REVISE
(acc[fn(val, i) ? 0 : 1].push(val), acc) 这段函数为什么要带acc 这参数呢?
要累加对象数组中包含的值.必须提供初始值,已遍各个item 可以正确的通过我的函数.
## USE
使用Array.prototype.reduce()和Array.prototype.push()根据filter向组添加元素。
## EXAMPLES 
```javascript
bifurcateBy(['beep', 'boop', 'foo', 'bar'], x => x[0] === 'b'); // [ ['beep', 'boop', 'bar'], ['foo'] ]
```