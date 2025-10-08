[Date.prototype.setDate() - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/setDate)

[2758. 下一天 - 力扣（LeetCode）](https://leetcode.cn/problems/next-day/)



<h2 id="EC1bC">题目描述</h2>
请你编写一个有关日期对象的方法，使得任何日期对象都可以调用 `date.nextDay()` 方法，然后返回调用日期对象的下一天，格式为 YYYY-MM-DD 。



```typescript
interface Date {
  nextDay(): string;
}

Date.prototype.nextDay = function (): string {
  /* 方式1 */ 
  // const oneDay = 24 * 60 * 60 * 1000; // 8.64e7
  // const date = new Date(this.getTime() + oneDay);
  // return date.toISOString().split('T')[0];

  /* 方式2(推荐) */
  const date = new Date(this);
  date.setDate(date.getDate() + 1); // Date 对象会自动处理跨越日期(标准做法)
  return date.toISOString().split('T')[0]; // YYYY-MM-DDTHH:mm:ss.sssZ
}

```



<details class="lake-collapse"><summary id="uadd10fc9"><strong><em><span class="ne-text">输入输出示例</span></em></strong></summary><p id="ud86df498" class="ne-p"><span class="ne-text">示例 1：</span></p><pre data-language="plain" id="u1euH" class="ne-codeblock language-plain"><code>输入：date = &quot;2014-06-20&quot;
输出：&quot;2014-06-21&quot;
解释：
const date = new Date(&quot;2014-06-20&quot;);
date.nextDay(); // &quot;2014-06-21&quot;</code></pre><p id="u03e7512c" class="ne-p"><span class="ne-text">示例 2：</span></p><pre data-language="plain" id="V5VEX" class="ne-codeblock language-plain"><code>输入：date = &quot;2017-10-31&quot;
输出：&quot;2017-11-01&quot;
解释：日期 2017-10-31 的下一天是 2017-11-01.</code></pre></details>
