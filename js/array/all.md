# all

## EXPLAIN 
如果提供的谓词函数对集合中的所有元素返回true，则返回true，否则返回false。
```javascript
const all = (arr, fn = Boolean) => arr.every(fn);
```
## REVISE
 
## USE
测试集合中的所有元素是否基于fn返回true。省略第二个参数fn，以使用布尔值作为默认值。
## EXAMPLES 
```javascript
all([4, 2, 3], x => x > 1); // true
all([1, 2, 3]); // true
```