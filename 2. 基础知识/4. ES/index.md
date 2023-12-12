# ES6 导航

先大致介绍 ES 的所有知识点，例如 let、Symbol、块级作用域等我称之为[ES6 完全指南](./ES6完全指南.md)

ES6 中最常见的面试题是 Promise，所以 Promise 首当其冲，我写下介绍 [Promise](./Promise.md) 是什么、[Promise 常见面试题](./Promise面试题.md)、再来一个[手写 Promise](./手写Promise.md)，Promise 大致上能明白个 7788。

说完 Promise，自然想到它的语法糖——[Async/Await](./Async.md)

再来了解一下[模块化历程](./模块化历程.md)

接下来是[Class](./Class.md)，它是面向对象编程的重要语法，在 JavaScript 早期是没有 Class 的，虽然在 ES6 时加上，但本质还是 prototype（原型）的语法糖

接着我们聊[迭代器和生成器](./Iterator&Generator.md)，看看循环时为什么会用到这个，他对 Async/Await 有什么影响

然后我们聊[Let&Const](./Let&Const.md)，在 ES6 之前，只有函数作用域和全局作用域，ES6 之后就有了块级作用域，块级作用域有什么用，它表示什么，Let 和 Const 能形成块级作用域，他们有什么区别，暂时性死区是什么？怎么影响，怎么作用

[Map 和 Set](./Map&Set.md)常考，Map 与 WeakMap 的区别，为什么手写拷贝一个对象需要用 WeakMap？Set 能起到去重的作用，它具体是怎么做的？

Proxy 是个很强大的功能，Vue3 就用此功能完成对数据的变化，我们这节来了解[Proxy](./Proxy.md)




## 我最常用的

ES6 的特性是使用最多的，包括类、模块化、箭头函数、函数参数默认值、模板字符串、解构赋值、延展操作符、Promise、let 与 const 等等，这部分已经是开发必备了，没什么好说的

另外还有：

-   ES7 的 `Array.prototype.includes()`
-   ES8 的 async/await 、String padding: `padStart()`和`padEnd()` 、 `Object.values()`
-   ES9 的 Rest/Spread 属性、for await of、 `Promise.finally()`
-   ES10 的 `Array.prototype.flat()` 、 `Array.prototype.flatMap()` 、String 的 `trimStart()` `trimEnd()`
-   ES11 的 `Promise.allSettled` 、空值处理及可选链
-   ES12 的逻辑赋值操作符、数字分隔符、 `Promise.any()`

## 最有用的

ES6 的特性都很有用，ES7-ES11 中，我比较感兴趣的是：

-   ES8 的 async/await
-   ES9 的 for await of
-   ES11 的 `Promise.allSettled` 、ES9 的 `Promise.finally()` 、ES12 的 `Promise.any()`
-   还有常用的逻辑操作：逻辑赋值操作符、数字分隔符、空值处理及可选链等都很大的简洁优化了我们的代码

其中，async/await 异步终极解决方案，`for await of` 异步串行，`Promise.allSettled` 解决了 `Promise.all` 的只要一个请求失败了就会抛出错误的问题，当我们一次发起多个请求时，所有结果都能返回，无论成功或失败，等等等，不了解的可以往下查找

## 参考资料

-   [从 ES6 到 ES10 的新特性万字大总结](https://zhuanlan.zhihu.com/p/342882092?utm_source=wechat_session&utm_medium=social&utm_oi=56197411504128)
-   [JS 之 ES7 详解](https://mp.weixin.qq.com/s/H6jUAGlkREM5SJgXc1Mjvw)
-   [盘点 ES12 中的一些新特性！](https://segmentfault.com/a/1190000041293383)
