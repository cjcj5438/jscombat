# 对象的深度克隆

## EXPLAIN 
```javascript
const deepClone = obj => {
  let clone = Object.assign({}, obj);
  Object.keys(clone).forEach(
      //TODO: 这段代码有点想不太明白  clone[key] =  obj[key] && typeof obj[key] === 'object'
    key => (clone[key] = typeof obj[key] === 'object' ? deepClone(obj[key]) : obj[key])
  );    
  // Array.from 是可以直接复制数组的;
  return Array.isArray(obj) ? (clone.length = obj.length) && Array.from(clone) : clone;
};
```
## REVISE

## USE
使用递归。使用object .assign()和一个空对象({})创建原始对象的浅克隆。使用Object.keys()和Array.prototype.forEach()来确定需要深度克隆哪些键值对。
## EXAMPLES 
```javascript
const a = { foo: 'bar', obj: { a: 1, b: 2 } };
const b = deepClone(a); // a !== b, a.obj !== b.obj
```
