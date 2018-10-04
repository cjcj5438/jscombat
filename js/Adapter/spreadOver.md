# 可定制的函数

## EXPLAIN 
一个可变函数并返回一个闭包，该闭包接受一个参数数组，以映射到函数的输入。
```javascript
const spreadOver = fn => argsArr => fn(...argsArr);
```
## REVISE
 
## USE
使用闭包和spread运算符(…)将参数数组映射到函数的输入。
## EXAMPLES 
```javascript
const arrayMax = spreadOver(Math.max);
arrayMax([1, 2, 3]); // 3
```