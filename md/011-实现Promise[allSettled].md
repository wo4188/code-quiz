[Promise.allSettled() - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/allSettled)

[2795. 并行执行 Promise 以获取独有的结果 - 力扣（LeetCode）](https://leetcode.cn/problems/parallel-execution-of-promises-for-individual-results-retrieval/description/)



<h2 id="EC1bC">题目描述</h2>
给定一个数组 `functions`，返回一个 promise 对象 `promise`。`functions` 是一个返回多个 promise 对象 `fnPromise` 的函数数组。每个 `fnPromise` 可以被解析（resolved）或拒绝（rejected）。

如果 `fnPromise` 被解析：

 `obj = { status: "fulfilled", value: resolved value}`

如果 `fnPromise` 被拒绝：

`obj = { status: "rejected", reason: 拒绝的原因（捕获的错误消息）}`

该 `promise` 应该返回一个包含这些对象 `obj` 的数组。数组中的每个 `obj` 应该对应原始函数数组中的多个 promise 对象，并保持相同的顺序。

请在不使用内置方法 `Promise.allSettled()` 的情况下实现它。



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

