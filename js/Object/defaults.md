# 对象中的属性指定默认值

## EXPLAIN 
为未定义的对象中的所有属性指定默认值。
```javascript
// 为什么这里要覆盖这么多 次 obj; 就是为了无缝 给属性添加默认值吗?
const defaults = (obj, ...defs) => Object.assign({}, obj, ...defs.reverse(), obj);
```
## REVISE
 Object.assign
 ...defs.reverse() 就是将数组里面的元素颠倒
## USE
使用object .assign()创建一个新的空对象，复制原始对象以保持键序，使用Array.prototype.reverse()和spread操作符…要将默认值从左到右组合起来，最后再次使用obj覆盖原来具有值的属性。
## EXAMPLES 
```javascript
defaults({ a: 1 }, { b: 2 }, { b: 6 }, { a: 3 }); // { a: 1, b: 2 }
```