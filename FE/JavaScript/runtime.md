# JS 运行时特性

- [隐式全局变量(opens new window)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/var#description)
- [变量提升(opens new window)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/var#变量提升)
- [暂时性死区(opens new window)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/let#暂存死区)
- [短路求值(opens new window)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Operator_Precedence#note_on_grouping_and_short-circuiting)
- [垃圾回收(opens new window)](https://zh.javascript.info/garbage-collection)

## 变量提升

`var` 声明的变量，可以在声明之前被使用，值为`undefined`

`function`声明的函数，可以在声明之前使用，但是函数表达式不行。

## 暂时性死区

`let` 和 `const` 声明的变量，在代码块执行到声明的变量行之前，变量都处于“暂时性死区”中。提前访问处在暂时性死区的变量会抛出 `ReferenceError` 错误。

## 垃圾回收

对于开发者来说，JavaScript 的内存管理是自动的、无形的。我们创建的原始值、对象、函数……这一切都会占用内存。

当我们不再需要某个东西时会发生什么？JavaScript 引擎如何发现它并清理它？

## [总结](https://zh.javascript.info/garbage-collection#zong-jie)

主要需要掌握的内容：

- 垃圾回收是自动完成的，我们不能强制执行或是阻止执行。
- 当对象是可达状态时，它一定是存在于内存中的。
- 被引用与可访问（从一个根）不同：一组相互连接的对象可能整体都不可达，正如我们在上面的例子中看到的那样。