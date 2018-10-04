# 异步函数转换promise对象

## EXPLAIN 
转换异步函数为promise对象
```javascript
const promisify = func => (...args) =>
  new Promise((resolve, reject) =>
   //这里要打断点来看. 不然不好理解的
   // 此时func 就是参数的函数:(d, cb) => setTimeout(cb, d) //cb是回调函数
    func(...args, (err, result) => (err ? reject(err) : resolve(result)))
  );
```
## REVISE
 
## USE
 promisify返回一个套用函数，再返回一个调用原始函数的promise。使用……rest运算符传递所有参数。
## EXAMPLES 
```javascript
const delay = promisify((d, cb) => setTimeout(cb, d));
delay(2000).then(() => console.log('Hi!')); // // Promise resolves after 2s
```