# base64编码

## EXPLAIN
base64 解码
```javascript
const btoa = str => Buffer.from(str, 'binary').toString('base64');
```
## REVISE

## USE

## EXAMPLES
```javascript
btoa('foobar'); // 'Zm9vYmFy'
```