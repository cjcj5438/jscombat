# 数组装换成cvs格式输出

## EXPLAIN 
将2D数组转换为逗号分隔值(CSV)字符串。
```javascript
const arrayToCSV = (arr, delimiter = ',') =>
  arr.map(v => v.map(x => `"${x}"`).join(delimiter)).join('\n');
```
## REVISE
 
## USE
使用Array.prototype.map()和Array.prototype.join(分隔符)将单个1D数组(行)组合成字符串。使用Array.prototype.join('\n')将所有行合并成CSV字符串，用换行符分隔每一行。省略第二个参数，分隔符，以使用默认的分隔符，
## EXAMPLES 
```javascript
arrayToCSV([['a', 'b'], ['c', 'd']]); // '"a","b"\n"c","d"'
arrayToCSV([['a', 'b'], ['c', 'd']], ';'); // '"a";"b"\n"c";"d"'
```