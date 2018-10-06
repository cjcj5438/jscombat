# 读取文件,一行一行的保存内容

## EXPLAIN
```javascript
const fs = require('fs');
const readFileLines = filename =>
  fs
    .readFileSync(filename)
    .toString('UTF8')
    .split('\n');
```
## REVISE

## USE

## EXAMPLES
```javascript
/*
contents of test.txt :
  line1
  line2
  line3
  ___________________________
*/
let arr = readFileLines('test.txt');
console.log(arr); // ['line1', 'line2', 'line3']
```