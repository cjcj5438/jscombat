# 判断是不是可读流

## EXPLAIN
```javascript
const isReadableStream = val =>
  val !== null &&
  typeof val === 'object' &&
  typeof val.pipe === 'function' &&
  typeof val._read === 'function' &&
  typeof val._readableState === 'object';
```
## REVISE

## USE

## EXAMPLES
```javascript
const fs = require('fs');
isReadableStream(fs.createReadStream('test.txt')); // true
```