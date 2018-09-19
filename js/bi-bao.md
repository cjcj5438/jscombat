# 闭包

# code1
```
function foo() {
    var a = 2;

    function bar() {
        console.log( a );
    }

    return bar;
}

var baz = foo();

baz(); // 2 ———— 朋友，这就是闭包的效果
```

# code2
```
function foo() {
    var a = 2;

    function baz() {
        console.log( a ); // 2
    }

    bar( baz );
}

function bar(fn) {
    fn(); // 妈妈快看呀，这就是闭包！
}
```

# code3
```
var fn;

function foo() {
    var a = 2;

    function baz() {
        console.log( a );
    }

    fn = baz; // 将baz分配给全局变量
}

function bar() {
    fn(); // 妈妈快看呀，这就是闭包！
}

foo();

bar(); // 2
```