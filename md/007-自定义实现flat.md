[Array.prototype.flat()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flat)



```javascript
// flat

Array.prototype.myFlat = function (depth = 1) {
  if (depth <= 0) return this.filter(() => true);

  return this.reduce((acc, cur) => {
    if (Array.isArray(cur)) {
      acc.push(...cur.myFlat(depth - 1));
    } else {
      acc.push(cur);
    }

    return acc;
  }, []);
};

const arr = [1, 2, , [[6, 7], , 8], 9];
arr.myFlat(2); // [1, 2, 6, 7, 8, 9]

// 🌈 filter/reduce 会跳过 稀疏数组的空槽 [1, ,2, , 3] => [1, 2, 3]
```

