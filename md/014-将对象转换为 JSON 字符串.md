[使用 JSON - 学习 Web 开发 | MDN](https://developer.mozilla.org/zh-CN/docs/Learn_web_development/Core/Scripting/JSON)

[2633. 将对象转换为 JSON 字符串 - 力扣（LeetCode）](https://leetcode.cn/problems/convert-object-to-json-string/description/)



<h2 id="EC1bC">题目描述</h2>
现给定一个值，返回该值的有效 JSON 字符串。你可以假设这个值只包括字符串、整数、数组、对象、布尔值和 null。返回的字符串不能包含额外的空格。键的返回顺序应该与 `Object.keys()` 的顺序相同。

请你在不使用内置方法 `JSON.stringify` 的前提下解决这个问题。



```typescript
// 只考虑这些 JSON 支持的类型
// 所有字符串只包含字母数字字符，不考虑转义之类的特殊情况
type JSONValue =
  | null //
  | boolean
  | number
  | string
  | JSONValue[]
  | { [key: string]: JSONValue };

function jsonStringify(object: JSONValue): string {
  switch (true) {
    case object === null:
    case typeof object === 'boolean':
    case typeof object === 'number':
      return '' + object;
    case typeof object === 'string':
      // 显式包裹 双引号，符合 JSON 的字符串规范
      return `"${object}"`;
    case Array.isArray(object):
      const arrStr = object.map(jsonStringify);
      return `[${arrStr}]`;
    default:
      const kvPairs = Object.keys(object).map(
        (x) => `"${x}":${jsonStringify(object[x])}` //
      );
      return `{${kvPairs}}`;
  }
}

```



<details class="lake-collapse"><summary id="u57d2d181"><em><strong><span class="ne-text">输入输出示例</span></strong></em></summary><p id="u371a31ff" class="ne-p"><span class="ne-text">示例 1：</span></p><pre data-language="plain" id="UrBcK" class="ne-codeblock language-plain"><code>输入：object = {&quot;y&quot;:1,&quot;x&quot;:2}
输出：{&quot;y&quot;:1,&quot;x&quot;:2}
解释：
返回该对象的 JSON 表示形式。
注意，键的返回顺序应该与 Object.keys() 的顺序相同。</code></pre><p id="u5f886d12" class="ne-p"><span class="ne-text">示例 2：</span></p><pre data-language="plain" id="prFK0" class="ne-codeblock language-plain"><code>输入：object = {&quot;a&quot;:&quot;str&quot;,&quot;b&quot;:-12,&quot;c&quot;:true,&quot;d&quot;:null}
输出：{&quot;a&quot;:&quot;str&quot;,&quot;b&quot;:-12,&quot;c&quot;:true,&quot;d&quot;:null}
解释：
JSON 的基本类型是字符串、数字型、布尔值和 null。</code></pre><p id="u92aa3f69" class="ne-p"><span class="ne-text">示例 3：</span></p><pre data-language="plain" id="cScKP" class="ne-codeblock language-plain"><code>输入：object = {&quot;key&quot;:{&quot;a&quot;:1,&quot;b&quot;:[{},null,&quot;Hello&quot;]}}
输出：{&quot;key&quot;:{&quot;a&quot;:1,&quot;b&quot;:[{},null,&quot;Hello&quot;]}}
解释：
对象和数组可以包括其他对象和数组。</code></pre><p id="u1ac52762" class="ne-p"><span class="ne-text">示例 4：</span></p><pre data-language="plain" id="IGsUT" class="ne-codeblock language-plain"><code>输入：object = true
输出：true
解释：
基本类型是有效的输入</code></pre><div class="ne-quote"></div></details>


