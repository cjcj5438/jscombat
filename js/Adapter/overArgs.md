# 参数转换之后再调用,提供函数

## EXPLAIN
创建一个函数，该函数使用转换后的参数调用所提供的函数。
 ```javascript
 // 代码思路非常精辟
const overArgs = (fn, transforms) =>
    (...args) =>
        // 这段比较难理解: fn(x,y)=>{[x,y]}
        // ...args.map((val, i) => transforms[i](val)) 的返回值是 两个值. 作为形参传给fn
        fn(...args.map((val, i) =>
            transforms[i](val)));
```
## USE
使用Array.prototype.map()与spread运算符(…)结合，将转换后的参数传递给fn。
用于对参数进行装换 然后在提供的函数使用装换后的参数.
## EXAMPLES
```javascript
const square = n => n * n;
const double = n => n * 2;
// 函数的参数可以这样写.函数式返回两个 参数
const fn = overArgs((x, y) => [x, y], [square, double]);
console.log(fn)
fn(9, 3); // [81, 6]
```