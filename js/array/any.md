# any

## EXPLAIN 
在一个集合中有最少有一个返回时true 时,则返回true ,否则返回false
```javascript
const any = (arr, fn = Boolean) => arr.some(fn);
```
## REVISE
 
## USE
使用Array.prototype.some()测试集合中的元素是否基于fn返回true。省略第二个参数fn，以使用布尔值作为默认值。
## EXAMPLES 
```javascript
any([0, 1, 2, 0], x => x >= 2); // true
any([0, 0, 1, 0]); // true
```