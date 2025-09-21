[2637. 有时间限制的 Promise 对象 - 力扣（LeetCode）](https://leetcode.cn/problems/promise-time-limit/description/)



```javascript
const timeLimit1 = (fn, t) => {
  return (...args) => {
    return new Promise((resolve, reject) => {
      const timer = setTimeout(() => {
        reject('超时了');
      }, t);

      fn(...args) //
        .then(resolve)
        .catch(reject)
        .finally(() => clearTimeout(timer));
    });
  };
};

const timeLimit2 = (fn, t) => {
  return (...args) => {
    let timer;
    const timeoutPromise = new Promise((resolve, reject) => {
      timer = setTimeout(() => {
        reject('超时了');
      }, t);
    });

    return Promise.race([
      fn(...args), //
      timeoutPromise,
    ]).finally(() => clearTimeout(timer));
  };
};


```

