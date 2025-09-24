[使用 JSON - 学习 Web 开发 | MDN](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Core/Scripting/JSON)

[typeof - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof)

[2628. 完全相等的 JSON 字符串 - 力扣（LeetCode）](https://leetcode.cn/problems/json-deep-equal/description/)



<h2 id="EC1bC">题目描述</h2>
给定两个对象 `o1` 和 `o2` ，请你检查它们是否 完全相等 。

对于两个 完全相等 的对象，必须满足以下条件：

+ 如果两个值都是原始类型，它们通过了 `===` 等式检查，则认为这两个值是 完全相等 的。
+ 如果两个值都是数组，在它们具有相同元素且顺序相同，并且每个元素在这些条件下也 完全相等 时，认为这两个值是 完全相等 的。
+ 如果两个值都是对象，在它们具有相同键，并且每个键关联的值在这些条件下也 完全相等 时，认为这两个值是 完全相等 的。

你可以假设这两个对象都是 `JSON.parse` 的输出。换句话说，它们是有效的 `JSON` 。

请你在不使用 lodash 的 `_.isEqual()` 函数的前提下解决这个问题。



```typescript
// 只考虑这些 JSON 支持的类型
// 不考虑 Date、function、undefined、NaN、Infinity‌、Symbol等
// 不考虑 循环引用 存在情况
type JSONValue =
  | null //
  | boolean
  | number
  | string
  | JSONValue[]
  | { [key: string]: JSONValue };

// 简单判断 2个值(有效 JSON) 是否完全相等
function areDeeplyEqual(o1: JSONValue, o2: JSONValue): boolean {
  // 如果两个值都是原始类型
  if ([o1, o2].every((x) => typeof x !== 'object')) {
    return o1 === o2;
  }

  if (typeof o1 !== typeof o2) return false;

  // 处理 typeof 无法区分的 null
  // 举例2: null === null ➡️➡️➡️ ✔️
  // 举例1: {} === null ➡️➡️➡️ ❌
  if (o1 === null && o2 === null) return true;
  if (o1 === null || o2 === null) return false;

  // 如果两个值都是数组
  if (Array.isArray(o1) && Array.isArray(o2)) {
    if (o1.length !== o2.length) false;

    for (let i = 0; i < o1.length; i++) {
      if (!areDeeplyEqual(o1[i], o2[i])) return false;
    }

    return true;
  }

  // 如果两个值都是对象
  if ([o1, o2].every((x) => !Array.isArray(x))) {
    const keys1 = Object.keys(o1);
    const keys2 = Object.keys(o2);

    // 检查两组键是否完全相同(与 顺序无关)
    if (keys1.length !== keys2.length) return false;
    if (!keys1.every((x) => keys2.includes(x))) return false;

    for (const key of keys1) {
      if (!areDeeplyEqual(o1[key], o2[key])) return false;
    }

    return true;
  }

  // 其他情况 按 false 处理
  // 举例1: {} === [] ➡️➡️➡️ ❌
  return false;
};
```



<details class="lake-collapse"><summary id="u57d2d181"><em><strong><span class="ne-text">输入输出示例</span></strong></em></summary><p id="ub9b8fdc9" class="ne-p"><span class="ne-text">示例 1：</span></p><pre data-language="plain" id="tqtQq" class="ne-codeblock language-plain"><code>输入：o1 = {&quot;x&quot;:1,&quot;y&quot;:2}, o2 = {&quot;x&quot;:1,&quot;y&quot;:2}
输出：true
输入：键和值完全匹配。</code></pre><p id="uccbdb070" class="ne-p"><span class="ne-text">示例 2：</span></p><pre data-language="plain" id="Ku4Gy" class="ne-codeblock language-plain"><code>输入：o1 = {&quot;y&quot;:2,&quot;x&quot;:1}, o2 = {&quot;x&quot;:1,&quot;y&quot;:2}
输出：true
解释：尽管键的顺序不同，但它们仍然完全匹配。</code></pre><p id="u913ed99a" class="ne-p"><span class="ne-text">示例 3：</span></p><pre data-language="plain" id="U2TeK" class="ne-codeblock language-plain"><code>输入：o1 = {&quot;x&quot;:null,&quot;L&quot;:[1,2,3]}, o2 = {&quot;x&quot;:null,&quot;L&quot;:[&quot;1&quot;,&quot;2&quot;,&quot;3&quot;]}
输出：false
解释：数字数组不同于字符串数组。</code></pre><p id="u7a05c9c2" class="ne-p"><span class="ne-text">示例 4：</span></p><pre data-language="plain" id="WuJOF" class="ne-codeblock language-plain"><code>输入：o1 = true, o2 = false
输出：false
解释：true !== false</code></pre><p id="uaac7d8f9" class="ne-p"><span class="ne-text"></span></p></details>


