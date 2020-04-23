# 奇技淫巧
> 可能不合理，但是逼格高！

## 数组去重
```javascript
let arr = [1,2,3,4,1,2,3,4]
arr = [...new Set(arr)]
```
## 数组乱序
```javascript
[1,2,3,4,5,6,7].sort(()=>Math.random()-0.5)
```