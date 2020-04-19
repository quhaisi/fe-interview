# 问题
实现函数curry, 要求完成如下功能
```javascript
function add(a, b, c) {
  return a + b + c
}
var add2 = curry(add);
console.log(add2(1, 2)(3)) // 6
console.log(add2(1)(2)(3)) // 6
```
# 分析
1. 高阶函数的应用：通过指定函数，生成一个新的函数
2. 满足一定条件，返回结果，而本题目的条件就是**参数的个数**
    >无论参数怎么组合，当输入参数总数大于等于形式参数的时候，返回结果

3. 拿到形式参数的个数，`Function.length`
    > 关于`Function.length`可以参考[MDN文档>Function 构造器](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/length)

# 解题
```javascript
const curry = fn => {
  const { length } = fn // 获取形参个数
  const curried = (...args) => {
    return (args.length >= length
      ? fn(...args) // 实参个数大于等于形参个数，执行目标函数fn
      : (...args2) => curried(...args.concat(args2))) // 否则返回一个新的函数，
      // 当该函数执行时会重新调用curried函数,并对参数进行合并，
      // 直到达成args.length >= length条件
  }
  return curried
}
```