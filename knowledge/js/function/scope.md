# 函数作用域
在函数内定义的变量不能在函数之外的任何地方访问，因为变量仅仅在该函数的域的内部有定义。相对应的，一个函数可以访问定义在其范围内的任何变量和函数。换言之，定义在全局域中的函数可以访问所有定义在全局域中的变量。在另一个函数中定义的函数也可以访问在其父函数中定义的所有变量和父函数有权访问的任何其他变量。


# 作用域

# 作用域链

函数执行的时候会创建AO
当函数执行完，gc会回收AO 所以局部变量就会被释放
active object (AO)临时创建的活动对象

# 闭包

html事件相当于浏览器的发布订阅事件，当事件被触发，由window去执行该事件

## 使用场景
1. 防抖、节流
2. 闭包模拟私有化（数据隐藏和封装）