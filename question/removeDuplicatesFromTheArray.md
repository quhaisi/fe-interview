# 数组去重

## ES6 Set去重
Set 对象允许你存储任何类型的唯一值，无论是原始值或者是对象引用。
Set的初始化允许传递一个**可迭代对象**，它的所有元素将不重复地被添加到新的Set中。
```javascript
// Use to remove duplicate elements from the array 
const numbers = [2,3,4,4,2,3,3,4,4,5,5,6,6,7,5,32,3,4,5]
console.log([...new Set(numbers)]) 
// [2, 3, 4, 5, 6, 7, 32]
```
## 双指针遍历数组
1. 对数组`arr`进行排序
2. 定义一个快指针`i`、一个慢指针`j`
3. 当`arr[i]===arr[j]`时，移动`j`指针跳过重复项
4. 当`arr[i]!==arr[j]`时，将`arr[j]`赋值给`arr[i+1]`，移动`j`指针
5. 当`j`超出数组长度，遍历结束，返回数组`0`到`i`的元素
```javascript
function removeDupl(arr) {
  let len = arr.length;
  if (len === 0 || len === 1) return arr;
  arr.sort();
  let i = 0,
    j = 1;
  while (j < len) {
    if (arr[i] !== arr[j]) {
      i++;
      arr[i] = arr[j];
    }
    j++;
  }
  return arr.slice(0, i + 1);
}
```

## `filter`过滤数组
`fliter`语法：
```javascript
var newArray = arr.filter(callback(element[, index[, array]])[, thisArg])
```
其中`index`是正在处理的元素在数组中的索引
可以通过`indexOf`取到数组中第一个元素的索引与`index`对比作为`filter`的`callback`的测试结果
```javascript
function removeDupl(arr) {
  return arr.filter(function(element, index) {
    return arr.indexOf(element) === index;
  });
}
```
## 双循环
嵌套`for`循环，或者利用`includes` `indexOf`等实现