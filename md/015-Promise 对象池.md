[Promise - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)

[2636. Promise 对象池 - 力扣（LeetCode）](https://leetcode.cn/problems/promise-pool/description/)



<h2 id="EC1bC">题目描述</h2>
<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);">请你编写一个异步函数</font><font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> </font>`<font style="color:rgba(38, 38, 38, 0.75);background-color:rgba(0, 10, 32, 0.03);">promisePool</font>`<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> </font><font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);">，它接收一个异步函数数组</font><font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> </font>`<font style="color:rgba(38, 38, 38, 0.75);background-color:rgba(0, 10, 32, 0.03);">functions</font>`<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> </font><font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);">和</font><font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> </font>**<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);">池限制</font>**<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> </font>`<font style="color:rgba(38, 38, 38, 0.75);background-color:rgba(0, 10, 32, 0.03);">n</font>`<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);">。它应该返回一个 promise 对象，当所有输入函数都执行完毕后，promise 对象就执行完毕。</font>

**<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);">池限制</font>**<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> </font><font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);">定义是一次可以挂起的最多 promise 对象的数量。</font>`<font style="color:rgba(38, 38, 38, 0.75);background-color:rgba(0, 10, 32, 0.03);">promisePool</font>`<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> </font><font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);">应该开始执行尽可能多的函数，并在旧的 promise 执行完毕后继续执行新函数。</font>`<font style="color:rgba(38, 38, 38, 0.75);background-color:rgba(0, 10, 32, 0.03);">promisePool</font>`<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> </font><font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);">应该先执行</font><font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> </font>`<font style="color:rgba(38, 38, 38, 0.75);background-color:rgba(0, 10, 32, 0.03);">functions[i]</font>`<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);">，再执行</font><font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> </font>`<font style="color:rgba(38, 38, 38, 0.75);background-color:rgba(0, 10, 32, 0.03);">functions[i + 1]</font>`<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);">，然后执行 </font>`<font style="color:rgba(38, 38, 38, 0.75);background-color:rgba(0, 10, 32, 0.03);">functions[i + 2]</font>`<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);">，等等。当最后一个 promise 执行完毕时，</font>`<font style="color:rgba(38, 38, 38, 0.75);background-color:rgba(0, 10, 32, 0.03);">promisePool</font>`<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> </font><font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);">也应该执行完毕。</font>

<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);">例如，如果</font><font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> </font>`<font style="color:rgba(38, 38, 38, 0.75);background-color:rgba(0, 10, 32, 0.03);">n = 1</font>`<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> </font><font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);">,</font><font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> </font>`<font style="color:rgba(38, 38, 38, 0.75);background-color:rgba(0, 10, 32, 0.03);">promisePool</font>`<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> 在序列中每次执行一个函数。然而，如果</font><font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> </font>`<font style="color:rgba(38, 38, 38, 0.75);background-color:rgba(0, 10, 32, 0.03);">n = 2</font>`<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> </font><font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);">，它首先执行两个函数。当两个函数中的任何一个执行完毕后，再执行第三个函数(如果它是可用的)，依此类推，直到没有函数要执行为止。</font>

<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);">你可以假设所有的 </font>`<font style="color:rgba(38, 38, 38, 0.75);background-color:rgba(0, 10, 32, 0.03);">functions</font>`<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> 都不会被拒绝。对于 </font>`<font style="color:rgba(38, 38, 38, 0.75);background-color:rgba(0, 10, 32, 0.03);">promisePool</font>`<font style="color:rgb(38, 38, 38);background-color:rgb(240, 240, 240);"> 来说，返回一个可以解析任何值的 promise 都是可以接受的。</font>



```typescript
type F = () => Promise<any>;

// 假设 functions 子项的 Promise返回值 都不会被拒绝
async function promisePool(functions: F[], n: number): Promise<any> {
  const pool = new Set<Promise<any>>();
  const results: any[] = [];

  for (const fn of functions) {
    if (pool.size >= n) {
      // 阻塞，开始排队，没空位就一直等
      await Promise.race(pool);
    }

    const task = fn();
    task.finally(() => pool.delete(task));
    pool.add(task);
    results.push(task);
  }

  // 此时 部分任务可能已经 fulfilled
  return Promise.all(results);
}

// const sleep = (t) => new Promise((res) => setTimeout(res, t));
// promisePool([() => sleep(500), () => sleep(400)], 1) //
//   .then(console.log); // After 900ms

```



<details class="lake-collapse"><summary id="uadd10fc9"><strong><em><span class="ne-text">输入输出示例</span></em></strong></summary><p id="ud86df498" class="ne-p"><span class="ne-text">示例 1：</span></p><pre data-language="plain" id="u1euH" class="ne-codeblock language-plain"><code>输入：
functions = [
  () =&gt; new Promise(res =&gt; setTimeout(res, 300)),
  () =&gt; new Promise(res =&gt; setTimeout(res, 400)),
  () =&gt; new Promise(res =&gt; setTimeout(res, 200))
]
n = 2
输出：[[300,400,500],500]
解释
传递了三个函数。它们的睡眠时间分别为 300ms、 400ms 和 200ms。
在 t=0 时，执行前两个函数。池大小限制达到 2。
当 t=300 时，第一个函数执行完毕后，执行第3个函数。池大小为 2。
在 t=400 时，第二个函数执行完毕后。没有什么可执行的了。池大小为 1。
在 t=500 时，第三个函数执行完毕后。池大小为 0，因此返回的 promise 也执行完成。</code></pre><p id="u03e7512c" class="ne-p"><span class="ne-text">示例 2：</span></p><pre data-language="plain" id="V5VEX" class="ne-codeblock language-plain"><code>输入：
functions = [
  () =&gt; new Promise(res =&gt; setTimeout(res, 300)),
  () =&gt; new Promise(res =&gt; setTimeout(res, 400)),
  () =&gt; new Promise(res =&gt; setTimeout(res, 200))
]
n = 5
输出：[[300,400,200],400]
解释：
在 t=0 时，所有3个函数都被执行。池的限制大小 5 永远不会满足。
在 t=200 时，第三个函数执行完毕后。池大小为 2。
在 t=300 时，第一个函数执行完毕后。池大小为 1。
在 t=400 时，第二个函数执行完毕后。池大小为 0，因此返回的 promise 也执行完成。</code></pre><p id="u3daec847" class="ne-p"><span class="ne-text">示例 3：</span></p><pre data-language="plain" id="H0ILm" class="ne-codeblock language-plain"><code>输入：
functions = [
  () =&gt; new Promise(res =&gt; setTimeout(res, 300)),
  () =&gt; new Promise(res =&gt; setTimeout(res, 400)),
  () =&gt; new Promise(res =&gt; setTimeout(res, 200))
]
n = 1
输出：[[300,700,900],900]
解释：
在 t=0 时，执行第一个函数。池大小为1。
当 t=300 时，第一个函数执行完毕后，执行第二个函数。池大小为 1。
当 t=700 时，第二个函数执行完毕后，执行第三个函数。池大小为 1。
在 t=900 时，第三个函数执行完毕后。池大小为 0，因此返回的 Promise 也执行完成。</code></pre></details>
