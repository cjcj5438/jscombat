# 判断是不是流

## EXPLAIN
```javascript
const isStream = val => val !== null && typeof val === 'object' && typeof val.pipe === 'function';
```
## REVISE

## USE

## EXAMPLES
```javascript
const fs = require('fs');
isStream(fs.createReadStream('test.txt')); // true
```