[comment]: //TODO性能优化学习，慕课网：让你页面速度飞起来
[TOC]
# 性能优化点
1. 网络层面
2. 构建层面
3. 服务端层面
4. 浏览器渲染层面

# 资源合并与压缩
1. html 压缩
2. css 压缩
3. js 压缩与混乱 (uglifyjs)
    1. 无效字符删除
    2. 剔除注释
    3. 代码语义缩减优化
    4. 代码保护
4. 文件合并
    优点：减少请求数量
    缺点：
      1. 首屏渲染问题
      2. 缓存失效问题
   
    解决办法：
      1. 公共库合并
      2. 不同页面单独打包（code-spite,异步组件）
# 图片相关优化
   1. 图片格式
      1. jpg有损压缩（解析过程） *不需要透明*
      2. png的格式 兼容性好
         1. png8   2^8 支持透明  *需要通明*
         2. png24  2^24 不支持透明
         3. png32  2^24 支持透明
      3. webp压缩程度更好，ios兼容性有问题，*安卓可用*
      4. svg矢量图，代码内嵌，相对较小，*场景简单 icon*
   2. 图片压缩
      1. 雪碧图
         + 雪碧图应该按业务拆分
         + [spritecow.com](http://www.spritecow.com/)雪碧图样式生成, 设置div背景，使用no-repeat做偏移，定义widht，height
      2. base64
      3. svg
      4. tinypng 图片压缩


# css与js
> 前提：浏览器如果渲染页面？
> 浏览器向服务器请求html文档，然后通过html parse把文档从上到下解析成DOM树，解析过程中如果遇到script、link标签，再去请求相应文件，css请求完毕，生成CSSOM树，再通过合并DOM树生成Render Tree
   1. html渲染过程的特点
      1. 顺序执行，并发加载（域名限制 静态资源托管到cdn）
   2. css阻塞
      + css head中阻塞页面的渲染
      + css阻塞js的执行
      + css不阻塞外部脚本的加载
   3. js阻塞
      + 直接引入的js阻塞页面的渲染
      + js不阻塞资源的加载（webkit有资源预加载的功能）
      + js顺序执行，阻塞后续js逻辑的执行（async defer）

# 懒加载与预加载
   1. 懒加载
      1. 图片进入可视区域加载图片
   2. 预加载
      1. 使用`img`标签，设置`display: none`
      2. 使用`new Image().src = "https://url"`
      3. 使用`xhr`请求
         好处：
         + 可使用progress进行数据传输监控

         坏处：
         + 存在跨域问题 
      4. 使用`preloadJS`

# 重绘与回流
   1. Javascript解析线程与UI渲染线程是互斥的
   2. 回流（reflow）：尺寸和布局的改变会触发回流
      1. 盒子模型相关属性的修改
      2. 定位属性及浮动
      3. 节点内部文字结构的修改
   3. 重绘（repaint）：外观的改变，不影响布局的属性改变触发重绘
   4. 新建DOM的过程：
      1. 获取DOM后分割成多个图层
      2. 对每个图层的节点计算样式结果（Recalculate style 样式重计算）
      3. 为每个节点生成图形和位置（Layout 回流和重布局）
      4. 将每个节点绘制填充到图层位图中（Paint Setup和Paint 重绘）
      5. 图层作为纹理上传至GPU
      6. 符合多个图层到页面上生成最终屏幕图像（Composite Layers 图层重组）
   5. 将频繁重回回流的DOM元素单独作为一个独立的图层（**不应该建立过多图层！！**）
      1. 3D或透视变换Css属性（perspective transform）
      2. 使用家属视频解码的\<video>节点
      3. 拥有3D（WebGL）上下文或加速的2D上下文的\<canvas>节点
      4. 混合插件（如flash）
      5. 对自己的opacity做css动画或使用一个动画webkit变换的元素
      6. 拥有加速CSS过滤器的元素（`transform:tranlateZ` `transform:tranlate3d(0,0,0)` `will-change:transform`等 GPU 3D 加速）
      7. 元素有一个包含复合层的后代节点
      8. 元素有一个z-index较低且包含一个复合层的兄弟元素
   6. 过度使用图层会把性能浪费在图层的合并上
   7. 优化点（**量化分析，前后对比**）
      1. 用translate替代top改变(translate不会触发回流)
      2. 用opacity替代visibility
         > `opacity`独占一个图层--使用`transform:tranlateZ`
         > `opacity`的改变是改变阿尔法通道的值，不会触发该图层的重绘和回流
      3. 通过改变DOM的className批量修改dom样式（flush缓冲区失效）
      4. DOM离线修改display: none之后修改样式，修改完成显示
      5. 不要在循环中访问DOM属性
      6. 不要使用table布局，可能一个小的改动会使整个table重新布局
      7. 合理的动画速度（css渲染会阻塞js线程）
      8. 对于动画新建图层
      9. 启用GPU硬件加速

# 浏览器存储
   1.cookie会在每一次的请求头中，当请求不需要cookie时（静态文件），会造成流量损耗。**解决办法**就是cdn部署静态资源，并且cdn域名和主站域名要分开。