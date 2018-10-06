# 移除数组不符合要求的元素

## EXPLAIN 
```javascript
 const compact = arr => arr.filter(Boolean);
```

## REVISE

## USE
使用Array.prototype.filter()来过滤掉falsey (false, null, 0, "", undefined, NaN).
## EXAMPLES 
```javascript
compact([0, 1, false, 2, '', 3, 'a', 'e' * 23, NaN, 's', 34]); // [ 1, 2, 3, 'a', 's', 34 ]
```