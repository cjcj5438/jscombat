# 一元函数

## EXPLAIN 
一个函数，该函数只接受一个参数，而忽略任何其他参数。
```javascript
const unary = fn => val => fn(val);
```
 
## USE
调用提供的函数fn，只给出第一个参数。
## EXAMPLES 
```javascript
['6', '8', '10'].map(unary(parseInt)); // [6, 8, 10]
```