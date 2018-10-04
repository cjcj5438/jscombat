# 数组元素是否全部相等

## EXPLAIN 
检查数组中的所有元素是否相等。
```javascript
const allEqual = arr => arr.every(val => val === arr[0]);
```
## REVISE
 
## USE
使用array .prototype.every()检查数组中的所有元素是否与第一个元素相同。
## EXAMPLES 
```javascript
allEqual([1, 2, 3, 4, 5, 6]); // false
allEqual([1, 1, 1, 1]); // true
```