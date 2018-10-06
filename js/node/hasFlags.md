# hasFlags

## EXPLAIN
检查进程是有指定标志
```javascript
const hasFlags = (...flags) =>
// /^-{1,2}/ 以^开始{1,2} 一个到两个, .test是返回时是否匹配成功.返回是boolean,
// 语义是先找到符合 --xxx 格式的正则然后再看是不是有要找的string对象.如果有那么就可以.如果没有那么就自动添加一个;
  flags.every(flag => process.argv.includes(/^-{1,2}/.test(flag) ? flag : '--' + flag));
```
## REVISE
array .prototype.include() 这个是数组的方法,是否包含返回值是boolean
## USE
使用array .prototype. every()和array .prototype.include()检查是否进行进程。argv包含所有指定的标志。使用正则表达式测试指定的标志是否带有-或-前缀，并相应地在它们前面加上前缀。
## EXAMPLES
```javascript
hasFlags('-s'); // true
hasFlags('--test', 'cool=true', '-s'); // true
hasFlags('special'); // false
```
```npm
node myScript.js -s --test --cool=true
```