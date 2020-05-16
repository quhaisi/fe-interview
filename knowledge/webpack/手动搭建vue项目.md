# 手动搭建 vue 项目

## Hello world

### 创建目录

```shell
mkdir vue-demo
cd vue-demo
npm init -y
```

### 安装 webpack

```shell
npm install webpack webpack-cli --save-dev
```

### 安装 vue、vue-loader、vue-template-compiler

```shell
npm install vue
npm install -D vue-loader vue-template-compiler
```

### webpack 配置

想要让`webpack`正确解析`.vue`文件，除了配置`vue-loader`外，还要配置`VueLoaderPlugin`插件。

新建`webpack.config.js`文件，配置如下：

```javascript
const VueLoaderPlugin = require("vue-loader/lib/plugin");

module.exports = {
  mode: "development",
  module: {
    rules: [
      {
        test: /\.vue$/,
        loader: "vue-loader",
      },
    ],
  },
  plugins: [new VueLoaderPlugin()],
};
```

新建`index.html` `index.js` `App.vue`文件

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="app"></div>
  </body>
  <script src="./dist/main.js"></script>
</html>
```

```javascript
// index.js
import Vue from "vue";
import App from "./App.vue";

new Vue({
  render: (h) => h(App),
}).$mount("#app");
```

```javascript
// App.vue
<template>
  <div>{{ msg }}</div>
</template>

<script>
export default {
  data() {
    return {
      msg: "Hello world!",
    };
  },
};
</script>
```

修改`package.json`文件，添加`scripts`指令：

```shell
"scripts": {
  - "test": "echo \"Error: no test specified\" && exit 1"
  + "dev": "webpack"
},
```
