# json保存成文件

## EXPLAIN
把json 数据保存为json文件
```javascript
const fs = require('fs');
const JSONToFile = (obj, filename) =>
  fs.writeFile(`${filename}.json`, JSON.stringify(obj, null, 2));

```
## REVISE

## USE

## EXAMPLES
```javascript
JSONToFile({ test: 'is passed' }, 'testJsonFile');
```