# 数组去重
```javascript
let arr = [1,2,3,4,1,2,3,4]
arr = [...new Set(arr)]
```
# 数组乱序
```javascript
[1,2,3,4,5,6,7].sort((a, b)=>(Math.random()>0.5?-1:1))
```