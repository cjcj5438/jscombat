# 将数组拆分成指定大小的数组

## EXPLAIN 
将数组拆分成指定大小的数组
```javascript
const chunk = (arr, size) =>
// 使用技巧:先定义数组的长度.然后在map 每个item对象; 人后在分别截取保存
  Array.from({ length: Math.ceil(arr.length / size) }, (v, i) =>
    arr.slice(i * size, i * size + size)
  );
// TODO: 为什么 会直接转换成二维数组
// 它为什么就会直接生成二维数组呢? 是因为slice 返回的是新数组
```
## REVISE
Math.ceil() 四舍五入
Array.from(数组对象, 新数组里面的每个item要执行的函数一般是这么用的;
 
## USE
使用array .from()来创建一个新的数组，它与将要生成的块数量相匹配。使用array .prototype.slice()将新数组的每个元素映射到大小为块的块。如果原始数组不能被平均分割，那么最后的块将包含其余的元素。
## EXAMPLES 
chunk([1, 2, 3, 4, 5], 2); // [[1,2],[3,4],[5]]
 