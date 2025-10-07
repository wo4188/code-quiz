[Array.prototype.forEach() - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

[Object.hasOwn() - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwn)

[2804. 数组原型的 forEach 方法 - 力扣（LeetCode）](https://leetcode.cn/problems/array-prototype-foreach/description/)



```javascript
// forEach

Array.prototype.myForEach = function (cb: (val: T, idx: number, arr: readonly T[]) => void, thisArg?: any) {
  const boundCb = thisArg //
    ? cb.bind(thisArg)
    : cb;

  for (let i = 0; i < this.length; i++) {
    // 跳过 稀疏数组项
    if (Object.hasOwn(this, i)) {
      boundCb(this[i], i, this);
    }
  }
};

const arr = [1, , 3, 4];
arr.myForEach((v, i, self) => console.log(v, i, self));
// 1 0 [1, 空白, 3, 4]
// 3 2 [1, 空白, 3, 4]
// 4 3 [1, 空白, 3, 4]
// undefined

```

