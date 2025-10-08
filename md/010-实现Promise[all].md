[Promise.all() - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)

[2721. 并行执行异步函数 - 力扣（LeetCode）](https://leetcode.cn/problems/execute-asynchronous-functions-in-parallel/description/)



```javascript
// Promise.all()

Promise.myAll = function (asyncFns) {
  return new Promise((resolve, reject) => {
    if (asyncFns.length === 0) {
      resolve([]);
      return;
    }

    const result = [];
    let count = 0; // 索引直接赋值时，若中间索引未赋值(‌稀疏)，length 属性不会自动更新

    for (let i = 0; i < asyncFns.length; i++) {
      asyncFns[i]()
        .then((res) => {
          result[i] = res; // 需要保持传入顺序，不要用 push
          if (++count === asyncFns.length) {
            resolve(result);
          }
        })
        .catch(reject);
    }
  });
};
```

