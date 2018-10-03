# flip~第一个参数方到最后


## EXPLAIN
Flip将一个函数作为参数，然后将第一个参数作为最后一个参数。
```javascript
const flip = fn => (first, ...rest) => fn(...rest, first);                                                          
```
## USE
返回一个接受可变输入的闭包;并在应用其他参数之前将最后一个参数拼接成第一个参数。


## EXAMPLES
```javascript
let a = { name: 'John Smith' };
let b = {};
const mergeFrom = flip(Object.assign);
let mergePerson = mergeFrom.bind(null, a);
mergePerson(b); // == b
b = {};
Object.assign(b, a); // == b
```