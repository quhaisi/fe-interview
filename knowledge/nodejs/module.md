node.js中的模块按引入方式分为三种：
1. [自定义模块](#custom)
2. [核心模块](#core)
3. [`node_modules`中的模块](#node_modules)

## <span id="custom">自定义模块</span>
在 Node.js 模块系统中，每个文件都被视为一个独立的模块。
文件的引入方式需要以'/'、 './' 或 '../' 开头：
```javascript
const foo = required('./foo.js')
```
当没有以 '/'、 './' 或 '../' 开头来表示文件时，这个模块必须是一个**核心模块**或**加载自`node_modules`目录**。

## <span id="core">核心模块</span>
核心模块定义在 Node.js 源代码的`lib/`目录下。
`require()`总是会优先加载核心模块。例如，`require('http')`始终返回内置的 HTTP 模块，即使有同名文件。所以当你要发布一个第三方模块的时候，一定要注意不要与核心模块同名。

## <span id="node_modules">`node_modules`中的模块</span>
`node_modules`中的模块通常是通过`npm install`安装的模块。
如果传递给`require()`的模块标识符不是一个核心模块，也没有以 '/' 、 '../' 或 './' 开头，则 Node.js 会从当前模块的父目录开始，尝试从它的`/node_modules`目录里加载模块。Node.js 不会附加`/node_modules`到一个已经以`/node_modules`结尾的路径上。

如果还是没有找到，则移动到再上一层父目录，直到文件系统的根目录。
例子，如果在`'/home/ry/projects/foo.js'`文件里调用了`require('bar.js')`，则 Node.js 会按以下顺序查找：
+ `/home/ry/projects/node_modules/bar.js`
+ `/home/ry/node_modules/bar.js`
+ `/home/node_modules/bar.js`
+ `/node_modules/bar.js`