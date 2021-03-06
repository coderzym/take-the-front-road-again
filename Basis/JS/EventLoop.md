1. 什么是事件循环？

因为JS这门语言是单线程的，为了避免出现阻塞后面代码执行的情况，就出现了事件循环，它是JS引擎执行时所遵循的一套规则：

   1. 首先JS文件在宏任务队列中开始执行，先执行JS的同步代码。
   2. 碰到微任务队列或者宏任务队列分别将它们压入各自的执行栈中等待同步代码执行完。
   3. 当同步代码执行完毕后，先清空微任务队列，在清空的过程中，如果又碰到了微任务和宏任务，则重复步骤二。
   4. 清空微任务后，再依次清空宏任务队列，如果又碰到了微任务和宏任务，则重复步骤二。

2. 在清空队列的过程中碰到了Web Worker事件怎么办？

`Web Worker`会单独开一个线程，所以不会有影响。

3. 微任务和宏任务分别有哪些？

    1. 微任务：`Promise.then`/`MutationObserver`
    2. 宏任务：`setTimeout`/`setInterval`/`I/O操作`

而这些都是由宿主环境，也就是浏览器来做的，会单独开辟一个线程。

4. requestAnimationFrame的执行时机是什么？

官方文档上讲的是发生在浏览器重绘之前。