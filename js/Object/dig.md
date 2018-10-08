# 属性挖掘

## EXPLAIN 
```javascript
const dig = (obj, target) =>
  target in obj
    ? obj[target]
    : Object.values(obj).reduce((acc, val) => {
        if (acc !== undefined) return acc;
        if (typeof val === 'object') return dig(val, target);
      }, undefined);
```
## REVISE
 Object.values(obj) 枚举所有的属性值
```javascript
var obj = { 0: 'a', 1: 'b', 2: 'c' };
console.log(Object.values(obj)); // ['a', 'b', 'c']

```
## USE
用in操作符检查obj中是否存在目标。如果找到，返回obj[target]的值，否则使用object .values(obj)和Array.prototype.reduce()递归地调用dig，直到找到第一个匹配的键/值对。
## EXAMPLES 
```javascript
const data = {
    level1: {
        level2: {
            level3: 'some data'
        }
    }
};
dig(data, 'level3'); // 'some data'
dig(data, 'level4'); // undefined
```