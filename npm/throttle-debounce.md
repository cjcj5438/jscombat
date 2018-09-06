# throttle-debounce

# 简单介绍 #
它提供了 throttle 和 debounce 两个函数：throttle 的含义是节流，debounce 的含义是防抖动，通过它们可以限制函数的执行频率，避免短时间内函数多次执行造成性能问题
# 用法 #
```
import { throttle, debounce } from 'throttle-debounce';

function foo() { console.log('foo..'); }
function bar() { console.log('bar..'); }

const fooWrapper = throttle(200, foo);

for (let i = 1; i < 10; i++) {
  setTimeout(fooWrapper, i * 30);
}

// => foo 执行了三次
// => foo..
// => foo..
// => foo..

const barWrapper = debounce(200, bar);

for (let i = 1; i < 10; i++) {
  setTimeout(barWrapper, i * 30);
}

// => bar 执行了一次 
// => bar..



```
# 源码学习 #
