[Array.prototype.lastIndexOf() - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/lastIndexOf)



```javascript
Array.prototype.myLastIndexOf = function (searchElement: any, fromIndex?: number): number {
  const len = this.length;
  let fromIdx = fromIndex ?? len - 1;

  if (len === 0) return -1;

  if (fromIdx < 0) {
    fromIdx = Math.max(-len, fromIdx) + len;
  } else {
    fromIdx = Math.min(len - 1, fromIdx);
  }

  // 需跳过数组的稀疏项(空项)，但保留显式的 [undefined]
  for (let i = fromIdx; i >= 0; i--) {
    if (Object.hasOwn(this, i) && this[i] === searchElement) {
      return i;
    }
  }

  return -1;
};

// [3,4,5].myLastIndexOf(5); // 2
// [3,4,5].myLastIndexOf('5'); // -1
// [3,4,,5].myLastIndexOf(undefined); // -1
// [3,3,undefined,4,5].myLastIndexOf(undefined); // 2
// [3,3,3,4,5].myLastIndexOf(3, 4); // 2
// [3,3,3,NaN,5].myLastIndexOf(NaN); // -1
```

