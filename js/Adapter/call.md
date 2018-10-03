# call

## EXPLAIN
给定一个键和一组参数，在给定上下文时调用它们。主要用于构图。

## USE
使用闭包调用带有存储参数的存储键。

## EXAMPLES
//  第一种使用                         
Promise.resolve([1, 2, 3])             
    .then(call('map', x => 2 * x))     
    .then(console.log); //[ 2, 4, 6 ]  
//  第二种使用                      
const map = call.bind(null, 'map');    
Promise.resolve([1, 2, 3])             
    .then(map(x => 2 * x))             
    .then(console.log); //[ 2, 4, 6 ]  