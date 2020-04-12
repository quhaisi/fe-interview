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

3. css与js
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

4. 懒加载与预加载
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