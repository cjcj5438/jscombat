# mimic-fn

# 简单介绍 #
mimic 的意思是模仿，它通过对原函数的复制从而模仿原函数的行为，可以在不修改原函数的前提下，扩充函数的功能。
# 用法 #
```
const mimicFn = require('mimic-fn');

function foo() {}
foo.date = '2018-08-27';

function wrapper() {
	return foo() {};
}

console.log(wrapper.name);
//=> 'wrapper'

// 此处复制 foo 函数后，
// foo 拥有的功能，wrapper 均有
mimicFn(wrapper, foo);

console.log(wrapper.name);
//=> 'foo'

console.log(wrapper.date);
//=> '2018-08-27'

```
# 源码介绍 #
```
'use strict';
module.exports = (to, from) => {
	// TODO: use `Reflect.ownKeys()` when targeting Node.js 6
	for (const prop of Object.getOwnPropertyNames(from).concat(Object.getOwnPropertySymbols(from))) {
		Object.defineProperty(to, prop, Object.getOwnPropertyDescriptor(from, prop));
	}

	return to;
};
// 源码其实很短,但是涉及 JavaScript 中非常核心基础的内容 —— property descriptor（属性描述符），还是值得好好研究一下的。
```

# 属性描述符介绍 #
> 形如 const obj = {x: 1} 是最简单的对象，x 是 obj 的一个属性。ES5 带给了我们对属性 x 进行定制化的能力。通过 Object.defineProperty(obj, 'x', descriptor) 可以实现一些有意思的效果：

## 不能被修改的属性 ##
```
const obj = {};

// 定于不能被修改的 x 属性
Object.defineProperty(obj, 'x', {
    value: 1,
    writable: false,//不能被修改的属性
    configurable: false,// 定义不能被删除的 y 属性
    enumerable: false,// 定义不能被遍历的 z 属性
    // 定义输入与输出不同的 u 属性
    get: function () {
        return this._u * 2;
    },
    set: function (value) {
        this._u = value;
    },
});
//不能被修改的属性
console.log(obj.x);
// => 1

obj.x = 2;
console.log(obj.x);
// => 1
// 定义不能被删除的 y 属性
console.log(obj.y);
// => 1

console.log(delete obj.y);
// => false

console.log(obj.y);
// => 1
// 定义不能被遍历的 z 属性
console.log(obj, obj.z);
// => {}, 1

for (const key in obj) {
    console.log(key, obj[key]);
}
// 定义输入与输出不同的 u 属性
obj.u = 1;
console.log(obj.u);

```

- defineProperty:方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性， 并返回这个对象
- defineProperties:方法直接在一个对象上定义一个或多个新的属性或修改现有属性，并返回该对象。
- getOwnPropertyDescriptor:该方法返回指定对象上一个自有属性对应的属性描述符。
- getOwnPropertyDescriptors:所指定对象的所有自身属性的描述符，如果没有任何自身属性，则返回空对象。
- getOwnPropertyNames
- getOwnPropertySymbols
- ownKeys


```
const obj= {
    x: 1,
    [Symbol('elvin')]: 2,
};

console.log(Object.getOwnPropertyNames(obj));
// => [ 'x' ]

console.log(Object.getOwnPropertySymbols(obj));
// => [ Symbol(elvin) ]

console.log(Reflect.ownKeys(obj));
// => [ 'x', Symbol(elvin) ]
```
另外对于 Node.js >= 6.0，可以通过 Reflect.ownKeys(obj) 的方式来实现同样的功能，而且代码更加的简洁，所以我尝试做了如下的更改：
```
module.exports = (to, from) => {
	for (const prop of Reflect.ownKeys(from)) {
		Object.defineProperty(to, prop, Object.getOwnPropertyDescriptor(from, prop));
	}

	return to;
};

```