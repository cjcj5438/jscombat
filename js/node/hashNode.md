# hash码

## EXPLAIN
使用SHA-256算法为值 创建hash。返回一个promise。
```javascript
const crypto = require('crypto');
const hashNode = val =>
  new Promise(resolve =>
    setTimeout(
      () =>
        resolve(
          crypto
            .createHash('sha256')
            .update(val)
            .digest('hex')
        ),
      0
    )
  );
```
## REVISE

## USE
使用crypto API为给定值创建hash。

## EXAMPLES
```javascript

hashNode(JSON.stringify({ a: 'a', b: [1, 2, 3, 4], foo: { c: 'bar' } })).then(console.log); 
// '04aa106279f5977f59f9067fa9712afc4aedc6f5862a8defc34552d8c7206393'
```