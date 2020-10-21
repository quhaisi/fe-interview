```javascript
function walk(time, cb) {
  let queue = [{ time, cb }];

  function execute() {
    if (queue.length > 0) {
      const { time, cb } = queue.shift();
      setTimeout(() => {
        cb();
        execute();
      }, time);
    }
  }
  execute();
  function walk(time, cb) {
    queue.push({ time, cb });
    return { walk };
  }
  return { walk };
}
function callback() {
  console.log("我被调用了");
}
walk(0, callback)
  .walk(2000, callback)
  .walk(1000, callback)
  .walk(1000, callback)
  .walk(1000, callback)
  .walk(1000, callback)
  .walk(1000, callback)
  .walk(1000, callback)
```