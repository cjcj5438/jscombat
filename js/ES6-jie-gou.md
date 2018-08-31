# ES6解构

# 简单的解构 #
## 数组 ##
```
let [a, b, c] = [0, 1, 2]
console.log(a, b, c) // 0 1 2
```
## 对象 ##
```javascript
//【将对象中属性的值赋给变量】
let obj = {a: 0, b: 1, c: 2}
// es5我们想把obj的值给取出来非常麻烦，而且obj的属性过多的话，还要进行遍历
let a = obj.a
let b = obj.b
let c = obj.c
// es6通过解构赋值就会非常简单
let {a: a, b: b, c: c} = obj
// 对象键值相同，可以只写一个【ES6提供的语法糖】，所以我们还可以简写成下面这个样子
let {a, b, c} = obj
console.log(a, b, c) // 0 1 2
```
## 模式匹配 ##
```
变量集合非对象和非数组 
let [a,b,c,d]=[1,2,3,4]
let {foo,bar}={foo:"aaa",bar:"bbb"}
```
# 解构赋值的常见特殊用法 #
## 给部分变量赋值 ##
```
//数组
let [a,,c,,e]=[1,2,3,4,5]
console.log(a,c,e)//1 3 5
// 不适用于对象
```

## 设置默认值 ##

```javascript
// 数组
let [a, b, c, d] = [1, 2, 3]
console.log(d) // undefined
// 这里的d未被赋值，所以值为undefined
// 在这种情况我们可以像对函数参数设置默认值一样，对d也设置默认值
let [a, b, c, d = 4] = [1, 2, 3]
console.log(d) // 4

// 对象
let {a = {}, b = 1} = {a: undefined, b: 10}
console.log(a, b) // {} 10

```
## 函数返回值结合 ##
```
// 数组
let f = () => [1, 2, 3]
let [a, b] = f()
console.log(a, b)

// 对象
let f = () => {
  return {a: 0, b: 1, c: 2}
}
let {a, b} = f()
console.log(a, b) // 0 1
```
## 与rest参数结合 ##
```
// 数组
let [a, ...args] = [10, 2, 3, 4, 5]
console.log(args) // [2, 3, 4, 5]
// 对象
let {a, ...args} = {a: 10, b: 5, c: 3}
console.log(args) // {b: 5, c: 3}
```
## 与函数参数结合 ##


## example ##
```
let obj = {a: 1, b: 2, c: {d: {e: 5}}}
let {a, b, c: {d}} = obj
console.log(d) 

```

```
function drawES2015Chart({size = 'big', cords = {x: 0, y: 0}, radius = 25} = {}) {
  console.log(size, cords, radius);
}

drawES2015Chart() // ?
drawES2015Chart({size: 'small', cords: {a: 1}, radius: {b: 1}}) // ?
```










