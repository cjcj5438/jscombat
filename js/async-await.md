# Async/Await

# 什么是async await #

- async/await是写异步代码的新方式，以前的方法有回调函数和
- Promise。
- async/await是基于Promise实现的，它不能用于普通的回调函数。
- async/await与Promise一样，是非阻塞的。
- async/await使得异步代码看起来像同步代码，这正是它的魔力所在。

# Async/Await语法 #
## promise ##
```
const makeRequestPromise = () => {
    getJSON()
        .then(data => {
            console.log(data)
            return "done"
        })
}
makeRequestPromise()
```
## Async / await ##
```
const makeRequestAsync = async () => {
    console.log(await getJSON())
    return "done"
}
makeRequestAsync()
```

## 细微不同 ##

1. 函数前面多了一个aync关键字。await关键字只能用在aync定义的函数内。async函数会隐式地返回一个promise，该promise的reosolve值就是函数return的值。(示例中reosolve值就是字符串"done")
2. 第1点暗示我们不能在最外层代码中使用await，因为不在async函数内。

# 为什么Async/Await更好？ #
## 简洁 ##
由示例可知，使用Async/Await明显节约了不少代码。我们不需要写.then，不需要写匿名函数处理Promise的resolve值，也不需要定义多余的data变量，还避免了嵌套代码。这些小的优点会迅速累计起来，这在之后的代码示例中会更加明显

## 错误处理 ##
Async/Await让try/catch可以同时处理同步和异步错误。在下面的promise示例中，try/catch不能处理JSON.parse的错误，因为它在Promise中。我们需要使用.catch，这样错误处理代码非常冗余。并且，在我们的实际生产代码会更加复杂。
```
const makeRequest = () => {
  try {
    getJSON()
      .then(result => {
        // JSON.parse可能会出错
        const data = JSON.parse(result)
        console.log(data)
      })
      // 取消注释，处理异步代码的错误
      // .catch((err) => {
      //   console.log(err)
      // })
  } catch (err) {
    console.log(err)
  }
}
```
使用aync/await的话，catch能处理JSON.parse错误:
```
const makeRequest = async () => {
  try {
    // this parse may fail
    const data = JSON.parse(await getJSON())
    console.log(data)
  } catch (err) {
    console.log(err)
  }
}
```
## 条件语句 ##