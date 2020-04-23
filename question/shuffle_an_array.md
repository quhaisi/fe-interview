# 数组乱序
## Fisher–Yates shuffle（洗牌算法）
从数组的最后一项开始遍历，随机从数组中取得一项（**包括自己**）与自己交换，然后向前遍历
```javascript
function shuffle(array) {
  let i = array.length;
  while (i > 1) {
    let random = Math.floor(Math.random() * i--);
    [array[random], array[i]] = [array[i], array[random]];
  }
}
```
## `Array.sort` + `Math.ramdom`方式
看似简单炫酷，实际也能实现打乱功能，就是不是很随机，几率发布的不均匀
```javascript
[1,2,3,4,5,6,7].sort(()=>Math.random()-0.5)
```

## 参考文献：
[「前端进阶」数组乱序](https://juejin.im/post/5d004ad95188257c6b518056#heading-7) 
[wiki/Fisher–Yates_shuffle](https://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle)