# 转换成绝对路径

## EXPLAIN
```javascript
const untildify = str => str.replace(/^~($|\/|\\)/, `${require('os').homedir()}$1`);
```
## REVISE
`${require('os').homedir()}$1` 这个是直接插入到 $1左边的. 好像闻到上面不能直接控制位置

## USE
使用String.prototype.replace()和OS.homedir()来将路径开头的~替换为主目录。
## EXAMPLES
```javascript
untildify('~/node'); // '/Users/aUser/node'
````