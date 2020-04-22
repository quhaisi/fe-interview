# 面试题
## css
+ [请说一下你知道的三栏布局](../src/css/layout/css-layout1.html)
+ [实现一个左右布局，左边固定100px，右边可伸缩，高度占满整个屏幕。右侧正中间有个长方形，宽高比2：1，宽是父元素的50%](../src/css/layout/css-layout2.html)

## js
+ [请说一下数组的reduce方法](../knowledge/js/array/reduce.md)
+ [如何做图片上传预览](../src/js/dom/图片预览.html)
+ [数组去重](../question/数组去重.js)
+ [打印对象o的某个属性为undifined， console.log(o)之后展开能却能看到该属性](../question/对象属性获取问题/README.md)
+ [基于Promise实现一个js/css加载器](../question/promise_file_loader)
+ [如何获取、修改伪元素的属性](../question/获取并修改伪元素的值.html)
+ [for...in循环遍历数组有什么缺点](../knowledge/js/array/for_in.md)
+ [实现函数curry, 要求完成如下功能](curry_function.md)
  <details>
    <summary>详细代码</summary>
    <pre>
      function add(a, b, c) {
        return a + b + c
      }
      var add2 = curry(add);
      console.log(add2(1, 2)(3)) // 6
      console.log(add2(1)(2)(3)) // 6
    </pre>
  </details>

## http
+ [你用过POST请求数据的哪些编码格式](../knowledge/http/编码请求主体.md)

## node.js
+ [谈谈你对node.js中模块的认识](../knowledge/nodejs/module.md)

## 算法
+ [如何判断链表是否循环]
+ [数组乱序]
+ [扁平化数组]