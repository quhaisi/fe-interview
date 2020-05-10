# Promise
## 含义
`Promise` 是一个对象，它代表了一个异步操作的最终完成或者失败。
## 特点
1. 对象的状态不受外界影响。Promise对象代表一个异步操作，有三种状态：`pending`（进行中）、`fulfilled`（已成功）和`rejected`（已失败）。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。
2. 一旦状态改变，就不会再变，任何时候都可以得到这个结果。 //TODO (如何保证状态不再改变？)
## 约定
在使用 `Promise` 时，会有以下约定：
+ 在本轮[事件循环](./event_loop.md)运行完成之前，回调函数是不会被调用的。
+ 即使异步操作已经完成（成功或失败），在这之后通过 `then()` 添加的回调函数也会被调用。
  ```javascript
  const a = new Promise((resolve, reject) => {
    setTimeout(function(){
      resolve('fulfilled')
    }, 1000)
  })
  a.then(value => {
    console.log(value) // fulfilled
  })
  setTimeout(function(){
    a.then(value => {
      console.log(value) // fulfilled
    })
  }, 2000)
  ```
+ 通过多次调用 `then()` 可以添加多个回调函数，它们会按照插入顺序执行。
  ```javascript
  const a = new Promise((resolve, reject) => {
    resolve('fulfilled')
  })
  a.then(value => {
    console.log(`No 1 ${value}`)
  })
  a.then(value => {
    console.log(`No 2 ${value}`)
  })
  a.then(value => {
    console.log(`No 3 ${value}`)
  })
  ```
  > No 1 fulfilled
  > No 2 fulfilled
  > No 3 fulfilled
## 链式调用（chaining）
连续执行两个或者多个异步操作是一个常见的需求，在上一个操作执行成功之后，开始下一个的操作，并带着上一步操作所返回的结果。**解决回调地狱的关键所在！**



