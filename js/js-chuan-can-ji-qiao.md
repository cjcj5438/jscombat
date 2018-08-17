# JS传参技巧

## 隐式创建 html 标签

```text
<input type="hidden" name="tc_id" value="{{tc_id}}">
```

{% hint style="info" %}
 这种方法一般配合ajax，上面的value使用了模板引擎
{% endhint %}

## window\['data'\]

```text
window['name'] = "the window object";
```

## 使用localStorage，cookie等存储

```text
window.localStorage.setItem("name", "xiaoyueyue");
window.localStorage.getItem("name")
```

{% hint style="warning" %}
1.localStorage 是持久存储，不主动删除 一直存在sessionStorage 是临时存储,关闭浏览器数据就没了 

2.localStorage 可以多窗口共享 sessionStorage 不能多窗口共享数据
{% endhint %}

## 获取地址栏方法

### 封装的方法

```text
function parseParam(url) {
  var paramArr = decodeURI(url).split("?")[1].split("&"),
    obj = {};
  for (var i = 0; i < paramArr.length; i++) {
    var item = paramArr[i];
    if (item.indexOf("=") != -1) {
      var tmp = item.split("=");
      obj[tmp[0]] = tmp[1];
    } else {
      obj[item] = true;
    }
  }
  return obj;

}
```

## 正则方法

```text
function GetQueryString(name) {
    var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
    var r = window.location.search.substr(1).match(reg);
    if (r != null) return unescape(r[2]); return null;
}
```

## 标签绑定函数传参

```text
<!--base-->
 <button id="test1" onclick="alert(id)">test1</button>
 
<!--高级-->
<button id="test" name="123" yue="xiaoyueyue" friend="heizi" onclick="console.log(this.getAttribute('yue'),this.getAttribute('friend'))">test</button>
 
```

### this拓展

 使用this传参，在使用art-template中琢磨出来的，再也不用只传递一个id拼接成好几个参数了！happy！

```text
var box = document.createElement("div");
    box.innerHTML =
      "<button id='1' data-name='xiaoyueyue' data-age='25' data-friend='heizi' onclick='alertInfo(this.dataset)'>点击</button>";
    document.body.appendChild(box);

    // name,age,friend
    function alertInfo(data) {
      alert('大家好,我是' + data.name + ', 我今年' + data.age + '岁了，我的好朋友是' + data.friend + ' !')
    }
```

{% hint style="warning" %}
 存储的data—含有大写的单词 =》这里会统一转化为小写，比如：data-orderId = “2a34fb64a13211e8a0f00050568b2fdd”，在实际取值的时候为`this.dataset.orderid`;
{% endhint %}

### event

 根据 class 获取当前的索引值，参数可以为 event对象

```text
var getIndexByClass =  function (param) {
    var element = param.classname ? param : param.target;
    var className = element.classname;
    var domArr = Array.prototype.slice.call(document.querySelectorAll('.' + className));
    for (var index = 0; index < domArr.length; index++) {
      if (domArr[index] === element) {
        return index;
      }
    }
    return -1;
  },
```

## HTML5 data-\* 自定义属性

```text
<button data-name="xiaoyueyue">点击</button>
```

```text
 var btn = document.querySelector("button")
    btn.onclick = function () {
      alert(this.dataset.name)
    }
```

## 字符串传参

### 单个参数

```text
var name = 'xiaoyueyue',
  age = 25;

var box = document.createElement("div");
box.innerHTML = '<button onclick="alertInfo(\'' + name + '\')">点击</button>';
document.body.appendChild(box);


// name, age
function alertInfo(name, age, home, friend) {
  alert("我是" + name)
}
```

### 多个参数

```text
var name = 'xiaoyueyue',
  age = '25',
  home = 'shanxi',
  friend = 'heizi';

var params = "&quot;" + name + "&quot;,&quot;" + age + "&quot;,&quot;" + home + "&quot;,&quot;" + friend + "&quot;";
var box = document.createElement("div");
box.innerHTML = "<button onclick='alertInfo(" + params + ")'>点击</button>";
document.body.appendChild(box);


// name, age,home,friend
function alertInfo(name, age, home, friend) {
  alert("我是" + name + ',' + "我今年" + age + "岁了！")
}
```

### 复杂传参

```text
var data = [
  {
    "name": "xiaoyueyue",
    "age": "25",
    "home": "shanxi",
    "friend": "heizi"
  }

]

var box = document.createElement("div");

for (var i = 0; i < data.length; i++) {
  box.innerHTML = "<button id='btn'  onclick='alertInfo(id,\"" + data[i].name + "\",\"" + data[i].age + "\",\"" + data[i].home + "\",\"" + data[i].friend + "\")'>点击</button>";
}

document.body.appendChild(box);

function alertInfo(id, name, age, home, friend) {
  alert("我是" + name + "," + friend + "是我的好朋友")
}
```

## arguments

{% hint style="info" %}
 `arguments`对象是所有（非箭头）函数中都可用的局部变量。你可以使用arguments对象在函数中引用函数的参数。它是一个类数组的对象
{% endhint %}

```text
<button onclick="fenpei('f233c7a290ae11e8a0f00050568b2fdd','100','0号 车用柴油(Ⅴ)')">分配</button>
```

```text
function fenpei() {
    var args = Array.prototype.slice.call(arguments);
    alert("我是" + args[2] + "油品，数量为 " + args[1] + " 吨， id为 " + args[0])

}
```

