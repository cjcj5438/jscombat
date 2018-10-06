# 数组不同元素

## EXPLAIN 
```javascript
const difference = (a, b) => {
    let s = new Set(b);
    s = a.filter(x => !s.has(x));
    return s
};
```

## USE
array.filter 是回返回需要的数组元素的,
然后new  Set() 是内部元素不能都相同的数据结构
## EXAMPLES 
```javascript
console.log(difference([1, 2, 3, 5, 6, 7], [1, 2, 4]))
```
