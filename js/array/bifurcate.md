# 根据bool来给数组分组

## EXPLAIN 
将值分成两组。如果filter中的元素是真实的，集合中的相应元素属于第一组;否则，它属于第二组。
```javascript
const bifurcate = (arr, filter) =>
// 纠正 这里的arr.reduce() 的两个参数: 参数一是回调函数.(acc[filter[i] ? 0 : 1].push(val), acc)
//                                  参数二是,初始值: [[], []]
// 以前一直理解错了.
// reduce 回调函数是可以接受四个参数,具体的https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce
  arr.reduce((acc, val, i) => (acc[filter[i] ? 0 : 1].push(val), acc), [[], []]);
```
## REVISE
 
## USE
使用Array.prototype.reduce()和Array.prototype.push()根据filter向组添加元素。
## EXAMPLES 
```javascript
bifurcate(['beep', 'boop', 'foo', 'bar'], [true, true, false, true]); 
// [ ['beep', 'boop', 'bar'], ['foo'] ]
```