# Module Methods
[//]: //TODO三种模块语法
## Webpack
除了上面描述的模块语法，webpack还允许一些自定义的、特定于webpack的方法:
### `require.context`
```javascript
require.context(
  directory: String,
  includeSubdirs: Boolean /* optional, default true */,
  filter: RegExp /* optional, default /^\.\/.*$/, any file */,
  mode: String  /* optional, 'sync' | 'eager' | 'weak' | 'lazy' | 'lazy-once', default 'sync' */
)
```
