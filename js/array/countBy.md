# 对数组元素进行分组,然后返回每组的元素的计数



## EXPLAIN 
对数组的元素进行分组，并返回每组元素的计数。

```javascript
const countBy = (arr, fn) =>
  arr.map(typeof fn === 'function' ? fn : val => val[fn]).reduce((acc, val, i) => {
      //如果有相同值就累加.每个item 的结果.为key ,然后 数量为 ++
    acc[val] = (acc[val] || 0) + 1;
    return acc;
  }, {});
```

## REVISE
reduce.的时候.如果是返回的事
## USE
使用array .prototype.map()将数组的值映射到函数或属性名。使用Array.prototype.reduce()创建一个对象，其中键是根据映射的结果生成的。

## EXAMPLES 
```javascript
countBy([6.1, 4.2, 6.3], Math.floor); // {4: 1, 6: 2}
countBy(['one', 'two', 'three'], 'length'); // {3: 2, 5: 1}
```
