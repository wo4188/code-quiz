[Array.prototype.unshift()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift)



```javascript
// unshift

Array.prototype.myUnshift = function () {
  for (let i = arguments.length - 1; i >= 0; i--) {
    this.splice(0, 0, arguments[i]);
  }

  return this.length;
};

const arr = [1, 2, 3];
console.log(arr.myUnshift(3, 4, 5)); // 6
console.log(arr); // [3, 4, 5, 1, 2, 3]

```

