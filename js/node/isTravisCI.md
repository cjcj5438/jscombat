# 判断是不是isTravisCI环境


## EXPLAIN
判断当前是不是TravisCI 环境;
```javascript
const isTravisCI = () => 'TRAVIS' in process.env && 'CI' in process.env;
```
## REVISE

## USE

## EXAMPLES
```
isTravisCI(); 
```