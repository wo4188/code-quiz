[Promise.allSettled() - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/allSettled)

[2795. 并行执行 Promise 以获取独有的结果 - 力扣（LeetCode）](https://leetcode.cn/problems/parallel-execution-of-promises-for-individual-results-retrieval/description/)



```javascript
// Promise.allSettled()

Promise.myAllSettled = function (asyncFns) {
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
          result[i] = {
            status: 'fulfilled',
            value: res,
          }; // 需要保持传入顺序，不要用 push
        })
        .catch((err) => {
          result[i] = {
            status: 'rejected',
            reason: err,
          };
        })
        .finally(() => {
          if (++count === asyncFns.length) {
            resolve(result);
          }
        });
    }
  });
};
```

