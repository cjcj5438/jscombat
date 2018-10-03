# call

## EXPLAIN
给定一个键和一组参数，在给定上下文时调用它们。主要用于构图。
```javascript
const call = (key, ...args) => context => {                 
    // context 是执行的上下文.可以是promise的data , 也可以是其他场景的上下文       
    context[key](...args);                                  
                                                            
}                                                           
```
## USE
使用闭包调用带有存储参数的存储键。

## EXAMPLES
//  第一种使用
```javascript
Promise.resolve([1, 2, 3])             
    .then(call('map', x => 2 * x))     
    .then(console.log); //[ 2, 4, 6 ]  
```                         

//  第二种使用  
```javascript
const map = call.bind(null, 'map');    
Promise.resolve([1, 2, 3])             
    .then(map(x => 2 * x))             
    .then(console.log); //[ 2, 4, 6 ]  
```                    
