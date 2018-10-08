# 深度冻结

## EXPLAIN 
```javascript
const deepFreeze = obj =>
  Object.keys(obj).forEach(
    prop =>
      !obj[prop] instanceof Object || Object.isFrozen(obj[prop]) ? null : deepFreeze(obj[prop])
  ) || Object.freeze(obj);
```
## REVISE
 
## USE
instanceof和typeof的区别
- typeof 返回的是一个字符串类型
- instanceof 返回boolean  比如:a instanceof Object a是谁的实例

## EXAMPLES 
```javascript

'use strict';

const o = deepFreeze([1, [2, 3]]);

o[0] = 3; // not allowed
o[1][0] = 4; // not allowed as well

```