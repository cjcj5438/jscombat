# 判断是不是双工流

## EXPLAIN
```javascript
const isDuplexStream = val =>
  val !== null &&
  typeof val === 'object' &&
  typeof val.pipe === 'function' &&
  typeof val._read === 'function' &&
  typeof val._readableState === 'object' &&
  typeof val._write === 'function' &&
  typeof val._writableState === 'object';
```
## REVISE

## USE
检查值是否与空值不同，使用typeof检查值是否为object类型，管道属性是否为function类型。另外，检查_read、_write和_readableState、_writableState属性的类型是否分别为函数和对象。
主要是用于在使用继承之后,判断是不是双工流
## EXAMPLES
```javascript
const Stream = require('stream');
isDuplexStream(new Stream.Duplex()); 
```