[Proxy - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy)

[2690. 无穷方法对象 - 力扣（LeetCode）](https://leetcode.cn/problems/infinite-method-object/description/)



<h2 id="EC1bC">题目描述</h2>
请你编写一个函数，返回一个 **无穷方法对象** 。

**无穷方法对象** 被定义为一个对象，它允许您调用任何方法，并始终返回方法的名称。

例如，如果执行 `obj.abc123()` ，它将返回 `"abc123"` 。



```typescript
function createInfiniteObject(): Record<string, () => string> {
  return new Proxy(
    // 要使用 Proxy 包装的目标对象
    //（可以是任何类型的对象，包括原生数组，函数，甚至另一个代理）
    {}, 
    {
      // 拦截对象的读取属性操作
      // target   ➡️ 目标对象
      // property ➡️ 被获取的属性名
      // receiver ➡️ Proxy 或者继承 Proxy 的对象
      get(target, property, receiver) {
        return () => String(property);
      }
    }
  )
};

/**
 * const obj = createInfiniteObject();
 * obj['abc123'](); // "abc123"
 */
```



<details class="lake-collapse"><summary id="uadd10fc9"><strong><em><span class="ne-text">输入输出示例</span></em></strong></summary><p id="ud86df498" class="ne-p"><span class="ne-text">示例 1：</span></p><pre data-language="plain" id="u1euH" class="ne-codeblock language-plain"><code>输入：method = &quot;abc123&quot;
输出：&quot;abc123&quot;
解释：
const obj = createInfiniteObject();
obj['abc123'](); // &quot;abc123&quot;
返回的字符串应始终与方法名称匹配。</code></pre><p id="u03e7512c" class="ne-p"><span class="ne-text">示例 2：</span></p><pre data-language="plain" id="V5VEX" class="ne-codeblock language-plain"><code>输入：method = &quot;.-qw73n|^2It&quot;
输出：&quot;.-qw73n|^2It&quot;
解释：返回的字符串应始终与方法名称匹配。</code></pre></details>
