# mem
2018/8/31 15:58:12 
# 简单介绍 #
缓存函数的返回值从而减少函数的实际执行次数，进而提升性能，当前版本为 3.0.1
# 用法 #
```javascript
const mem = require('mem');

// 同步函数缓存
let i = 0;
const counter = () => ++i;
const memoized = mem(counter);

memoized('foo');
//=> 1

memoized('foo');
//=> 1   参数相同，返回换成的结果 1

memoized('bar');
//=> 2   参数变化，counter 函数再次执行，返回 2

memoized('bar');
//=> 2

// 异步函数缓存
let j = 0;
const asyncCounter = () => Promise.resolve(++j);
const asyncmemoized = mem(asyncCounter);

asyncmemoized().then(a => {
    console.log(a);
    //=> 1

    asyncmemoized().then(b => {
        console.log(b);
        //=> 1
    });
});


```
> 除此之外它还支持 设置缓存时间、自定义缓存 Hash 值、统计缓存命中数据等功能。

# 源码学习 #
## 哈希函数 ##
为了让mem 处理过的函数对于相同的参数能返回相同的值,那么就必须对参数进行hash处理,然后将哈希结果作为key ,函数运行结果作为value,缓存起来
```
const cache = {};

// 缓存 arg1 的运行结果
const key1 = getHash(arg1);
cache[key1] = func(arg1);

// 缓存 arg2 的运行结果
const key2 = getHash(arg2);
cache[key2] = func(arg2);
```

那其中关键的问题在于这哈希函数,如何处理不同的数据类型,如何处理对象间的比较,其实这也是面试中经常被问到的,如何进行深比较: 来看源码
```
// mem 的哈希函数
const defaultCacheKey = (...args) => {
	if (args.length === 1) {
		const [firstArgument] = args;
		if (
			firstArgument === null ||
			firstArgument === undefined ||
			(typeof firstArgument !== 'function' && typeof firstArgument !== 'object')
		) {
			return firstArgument;
		}
	}

	return JSON.stringify(args);
};
// 它做了什么当只有一个参数的时候.且参数为 null | undefined 或者类型不为 function | object 时，哈希函数直接将参数返回。
// 若不是上述情况，则返回参数经过 JSON.stringify() 的值。
```
现在我们复习下 ES6 中定义的数据类型.（Boolean | Nunber | Null | Undefined | String| Symbol）和 Object 类型。
```
const object1 = {a: 1};
const object2 = {a: 1};

console.log(object1 === object2);
// => flase

// 期望效果 用mem 的hash 函数defaultCacheKey
console.log(defaultCacheKey(object1) === defaultCacheKey(object2));
// => true
```
好了, 继续  一开始 我会以为会用类似Lodash 的 _.isEqual() 实现 ,没想到会直接使用Object类型的数据通过JSON.stringify() 转化为字符串后进行处理！ 有点惊呆,这种方法简单,可读性好但是会出新问题
1. 当对象结构复杂时，JSON.stringify() 会消耗不少时间
	1. 还好，因为假如通过 JSON.stringify() 哈希时，性能存在问题的话，mem 支持传入自定义的哈希函数，可以通过自行编写高效哈希函数进行解决。
2. 对于不同的正则对象，JSON.stringify() 的结果均为 {}，与哈希函数的预期效果不符
	1. 属于函数功能不符合预期，需要进行 bugfix。
	```
	console.log(JSON.stringify(/Sindre Sorhus/));
	// => '{}'
	
	console.log(JSON.stringify(/Elvin Peng/));
	// => '{}'
	```

## 存储结构 ##
不考虑额外参数时，对于同步函数的支持源代码可简化如下：
```javas
// 源代码 2-2 mem 核心逻辑
const mimicFn = require('mimic-fn');

/*
WeakMap 和 map 的区别
GC机制:只要外部调用,内部直接垃圾回收
只能是对象和数组提供的方法要比map少多
*/
const cacheStore = new WeakMap();

module.exports = (fn) => {
    const memoized = function (...args) {
		// 拿到weakMap对象的数据中 memoized执行结果的
        const cache = cacheStore.get(memoized);
		// 参数对象
        const key = defaultCacheKey(...args);

        // 这句是什么意思?么理解
        if (cache.has(key)) {
            const c = cache.get(key);
            return c.data;
        }
		// 调用fn 函数,同时把...args 参数传递
        const ret = fn.call(this, ...args);
        // 规定时间下 添加对象到 cache 中
        const setData = (key, data) => {
            cache.set(key, {
                data,
            });
        };
        
        setData(key, ret);
        //返回 新函数
        return ret;
    }
    
	//将类型为 Map 的 retCache 作为函数执行结果的缓存
	//缓存的键值为 defaultCacheKey 哈希后的结果。
    const retCache = new Map();
   
    mimicFn(memoized, fn);

    cacheStore.set(memoized, retCache);

    return memoized;
}

```
retCache 选用 Map 类型而不用 Object 类型主要是因为 Map 的键值支持所有类型，而 Object 的键值只支持字符串，除此之外，关于缓存数据结构优选选择 Map 类型还有以下优点：

Map.size 属性可以方便的获得当前缓存的个数
Map 类型支持 clear() | forEach() 等常用的工具函数
Map 类型是默认可迭代的，即支持 iterable protocol

cacheStore 选用 WeakMap 类型而不用 Map 类型主要是因为其具有不增加引用个数的优点，更有利于 Node.js 引擎的垃圾回收。

