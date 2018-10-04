# 管道同步函数

## EXPLAIN
 执行从左到右的函数组合。
```javascript
const pipeFunctions = (...fns) => fns.reduce((f, g) => (...args) => g(f(...args)));
```

## REVISE
reduce 有一个参数的时候,表示一个累计的结果.是一个callback()

## USE
使用Array.prototype.reduce()和spread操作符(…)一起执行从左到右的函数组合。
第一个(最左)函数可以接受一个或多个参数;其余的函数必须是一元函数。
 
## EXAMPLES 
```javascript
const add5 = x => x + 5;
const multiply = (x, y) => x * y;
const multiplyAndAdd5 = pipeFunctions(multiply, add5);
multiplyAndAdd5(5, 2); // 15
```