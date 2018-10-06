# 数组元素某元素计数

## EXPLAIN 
计数数组中出现的值。

```javascript
const countOccurrences = (arr, val) => arr.reduce((a, v) => (v === val ? a + 1 : a), 0);
```

## USE
每次在数组中遇到特定值时，使用array. prototype.reduce()增加计数器的值。
## EXAMPLES 
```javascript
const countOccurrences = (arr, val) => arr.reduce((a, v) => (v === val ? a + 1 : a), 0);

```
