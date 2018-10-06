# 判断是不是可写流

## EXPLAIN
```javascript
const isWritableStream = val =>
  val !== null &&
  typeof val === 'object' &&
  typeof val.pipe === 'function' &&
  typeof val._write === 'function' &&
  typeof val._writableState === 'object';
```
## REVISE

## USE

## EXAMPLES
```javascript
const fs = require('fs');
isWritableStream(fs.createWriteStream('test.txt')); 
```