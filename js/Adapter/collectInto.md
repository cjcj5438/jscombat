# ChangesFN,可变参函数

## EXPLAIN
将接受数组的函数,最后的结果集合到数组中;
```javascript
const collectInto = fn => (...args) => {
    console.log(args)
    return fn(args);
}
```

## USE
给定一个函数，返回一个闭包，该闭包将所有输入收集到一个数组接受函数中。

## EXAMPLES
```javascript
// todo:用处是this 绑定.如果不绑定那么就会到全局找fn
const Pall = collectInto(Promise.all.bind(Promise));
let p1 = Promise.resolve(1);
let p2 = Promise.resolve(2);
let p3 = new Promise(resolve => setTimeout(resolve, 2000, 3));
Pall(p1, p2, p3).then(console.log); // [1, 2, 3] (after about 2 seconds)
```
问是不是只有带promise 中才能这样使用呢? 显然不是;