# Promise {code}

## promise chain\(方法链\)

```javascript
function taskA() {
    console.log("task A")
    throw  new Error("throw error @ task a")
}

function taskB() {
    console.log("task B")
}

function onRejected(err) {
    console.log(err)
}

function finalTask() {
    console.log("final task")
}

var promise = Promise.resolve()
promise
    .then(taskA)//执行
    .then(taskB)//出现错误跳过这个步骤
    .catch(onRejected)//捕获taskA的错误
    .then(finalTask)//最后执行的函数
```

## 传参数

```text
//如果此时taskA 要传递参数那么直接return 即可， 在执行到taskB的时候，就会拿到参数


function doubleUp(value) {
    return value * 2;
}

function increment(value) {
    return value + 1;
}

function output(value) {
    console.log(value)
}

let promise2 = Promise.resolve(1);
promise2
    .then(increment)//2
    .then(doubleUp)//4
    .then(output)//console.log(4)
    .catch(function (err) {
        // 当出现错误的时候会被调用
        console.log(err)
    })

```

## Promise\#catch

```text
// Promise#catch
// IE 8浏览器实用catch（ECMAScript3保留字）作为属性会出现 identifier not found，ECMAScript5保留字可以作为属性
//1.用 catch标识符解决冲突问题

var promise = Promise.reject(new Error("message"));
promise["catch"](function (error) {
    console.error(error);
});
// 2.改用then代替

var promise = Promise.reject(new Error("message"));
promise.then(undefined, function (error) {
    console.error(error);
});

//正确的 返回返回新创建的promise对象
function anAsyncCall() {
    var promise = Promise.resolve();
    return promise.then(function () {
        // 任意处理
        return newVar;
    });
}
```

## 使用Promise\#then同时处理多个异步请求

```text
// 一个异步请求
function getURL() {
    return new Promise(function (resolve, reject) {
        setTimeout(function () {
            resolve('Async Hello world');
        }, 16);
    });
}

// request 中含有两个请求方法
var request = {
    comment() {
        return getURL().then((a) => {
            JSON.parse(a)
        });
    },
    people() {
        return getURL().then((a) => {
            JSON.parse(a)
        });
    }
};

function main() {
    function recordValue(results, value) {
        results.push(value);
        return results;
    }

    // [] 用来保存初始化的值
    var pushValue = recordValue.bind(null, []);// 这里语法要查阅资料
    return request.comment().then(pushValue).then(request.people)
        // .then(pushValue);这步可以不要了, 我举得
}

// 运行的例子
main().then(function (value) {
    console.log(value);
}).catch(function (error) {
    console.log(error);
});
```

## Promise.all

```text
// 把上面的方法 main 的方法修该下
function main() {
    return Promise.all([request.comment(), request.people()]);
}
```

## Promise.race

```text
let p1 = new Promise((resolve, reject) => {
    setTimeout(() => {
        console.log(1)
        resolve('成功了')
    }, 2000);
})

let p2 = new Promise((resolve, reject) => {
    setTimeout(() => {
        console.log(2)
        resolve('success')
    }, 5000);
})

/*只会返回第一个成功的值*/
Promise.race([p1, p2]).then((result,result2) => {
    console.log(result,result2)
}).catch((error) => {
    console.log(error)
})
```

