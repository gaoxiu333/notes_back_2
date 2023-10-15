# Function

三种在 JavaScript 中创建函数的方式：

1. 函数声明：主代码流中的函数
2. 函数表达式：表达式上下文中的函数
3. 箭头函数：

> - 函数可能具有局部变量：在函数内部声明的变量，或在其参数列表中。这类变量只在函数内部可见。
> - 参数可以有默认值：`function sum(a = 1, b = 2) {...}`。
> - 函数总是返回一些东西。如果没有 `return` 语句，那么返回的结果是 `undefined`。

## 杂项

杂项

- [`arguments`(opens new window)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/arguments)
- [`.name`(opens new window)](https://zh.javascript.info/function-object#shu-xing-name)
- [`.length`(opens new window)](https://zh.javascript.info/function-object#shu-xing-length)
- [IIFE (opens new window)](https://zh.javascript.info/var#iife)“立即执行函数表达式” `(() => {})()`
- [callback (opens new window)](https://zh.javascript.info/callbacks)“回调函数”
- [`globalThis`(opens new window)](https://zh.javascript.info/global-object)
- [尾调用优化](https://wangdoc.com/es6/function.html#尾调用优化)

## 函数绑定

- call 

  - ```js
    function.call(thisArg, arg1, arg2, ...)
    ```

- Apply

  - ```js
    apply(thisArg)
    apply(thisArg, argsArray)
    ```

- bind

  - ```js
    function.bind(thisArg[, arg1[, arg2[, ...]]])
    ```

## 递归和堆栈

- **递归** 是编程的一个术语，表示从自身调用函数（译注：也就是自调用）。递归函数可用于以更优雅的方式解决问题。

  当一个函数调用自身时，我们称其为 **递归步骤**。递归的 **基础** 是函数参数使任务简单到该函数不再需要进行进一步调用。

- [递归定义](https://en.wikipedia.org/wiki/Recursive_data_type) 的数据结构是指可以使用自身来定义的数据结构。

- 任何递归函数都可以被重写为迭代（译注：也就是循环）形式。有时这是在优化代码时需要做的。但对于大多数任务来说，递归方法足够快，并且容易编写和维护。

> 递归的缺点？

## 函数的参数 rest 和 spread

当我们在代码中看到 `"..."` 时，它要么是 rest 参数，要么是 spread 语法。

有一个简单的方法可以区分它们：

- 若 `...` 出现在函数参数列表的最后，那么它就是 rest 参数，它会把参数列表中剩余的参数收集到一个数组中。
- 若 `...` 出现在函数调用或类似的表达式中，那它就是 spread 语法，它会把一个数组展开为列表。

使用场景：

- Rest 参数用于创建可接受任意数量参数的函数。
- Spread 语法用于将数组传递给通常需要含有许多参数的函数。

我们可以使用这两种语法轻松地互相转换列表与参数数组。

旧式的 `arguments`（类数组且可迭代的对象）也依然能够帮助我们获取函数调用中的所有参数。

## 函数对象

函数的类型是对象。通常它包含一下两个属性。

- `name` —— 函数的名字。通常取自函数定义，但如果函数定义时没设定函数名，JavaScript 会尝试通过函数的上下文猜一个函数名（例如把赋值的变量名取为函数名）。
- `length` —— 函数定义时的入参的个数。Rest 参数不参与计数。

如果函数是通过函数表达式的形式被声明的（不是在主代码流里），并且附带了名字，那么它被称为命名函数表达式（Named Function Expression）。这个名字可以用于在该函数内部进行自调用，例如递归调用等。

## 作用域和闭包

作用域：

- 代码块 `{...}`
- 函数

#### 词法环境

在 JavaScript 中，每个运行的函数，代码块 `{...}` 以及整个脚本，都有一个被称为 **词法环境（Lexical Environment）** 的内部（隐藏）的关联对象。

法环境对象由两部分组成：

1. **环境记录（Environment Record）** —— 一个存储所有局部变量作为其属性（包括一些其他信息，例如 `this` 的值）的对象。
2. 对 **外部词法环境** 的引用，与外部代码相关联。

> 函数声明一开始就会放在 司法环境 内。
>
> **当代码要访问一个变量时 —— 首先会搜索内部词法环境，然后搜索外部环境，然后搜索更外部的环境，以此类推，直到全局词法环境。**

#### 闭包

定义：

[闭包](https://en.wikipedia.org/wiki/Closure_(computer_programming)) 是指一个函数可以记住其外部变量并可以访问这些变量。在某些编程语言中，这是不可能的，或者应该以一种特殊的方式编写函数来实现。但如上所述，在 JavaScript 中，所有函数都是天生闭包的（只有一个例外，将在 ["new Function" 语法](https://zh.javascript.info/new-function) 中讲到）。

原理：

所有的函数在“诞生”时都会记住创建它们的词法环境。词法环境保存了创建该函数的词法环境引用。

影响：

闭包影响垃圾回收，通常函数被推出调用栈后，会从调用栈清除，但闭包函数引用的词法环境不会被清除掉。



## 箭头函数

- 没有 `this`
- 没有 `arguments`
- 不能使用 `new` 进行调用
- 它们也没有 `super`

箭头函数是针对那些没有自己的“上下文”，但在当前上下文中起作用的短代码的。并且箭头函数确实在这种使用场景中大放异彩。

## 调度 setTimeout 和 setInterval

- `setTimeout(func, delay, ...args)` 和 `setInterval(func, delay, ...args)` 方法允许我们在 `delay` 毫秒之后运行 `func` 一次或以 `delay` 毫秒为时间间隔周期性运行 `func`。
- 要取消函数的执行，我们应该调用 `clearInterval/clearTimeout`，并将 `setInterval/setTimeout` 返回的值作为入参传入。
- 嵌套的 `setTimeout` 比 `setInterval` 用起来更加灵活，允许我们更精确地设置两次执行之间的时间。
- 零延时调度 `setTimeout(func, 0)`（与 `setTimeout(func)` 相同）用来调度需要尽快执行的调用，但是会在当前脚本执行完成后进行调用。
- 浏览器会将 `setTimeout` 或 `setInterval` 的五层或更多层嵌套调用（调用五次之后）的最小延时限制在 4ms。这是历史遗留问题。

请注意，所有的调度方法都不能 **保证** 确切的延时。

例如，浏览器内的计时器可能由于许多原因而变慢：

- CPU 过载。
- 浏览器页签处于后台模式。
- 笔记本电脑用的是省电模式。

所有这些因素，可能会将定时器的最小计时器分辨率（最小延迟）增加到 300ms 甚至 1000ms，具体以浏览器及其设置为准。
