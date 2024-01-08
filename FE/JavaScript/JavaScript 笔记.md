

## 新增特性

- `??` - 空值合并
- `?.` - 可选链
- 新的赋值运算 - `a ||= b` 、`a ??= b`
- BigInt - `10n`、`BigInt(10)`、`BigInt(’10‘)`
- Generator - `function* fn(){yeid 1}`
- class 私有属性 - `Class A{ #val = 2; }`

## 严格模式

提供更严格的错误检查和更安全的编程环境的方式。启用严格模式可以帮助你避免某些常见的编程错误，提高代码的运行效率

**作用**
- 变量必须声明
- 禁止使用`with`
- 保留字
- `this` 指向 - 没有指定环境的函数`this`指向`undefined`
- 操作被属性描述符限制的属性，抛出错误，比如 删除，重复属性名等

**如何使用**
- `use strict`
	- 放置在脚本最顶部
	- 函数体顶部
	- ES6 模块默认开启


----

## 基础知识

### 数据类型

- 七种原始数据类型
	- `string`,`number`,`boolean`,`null`,`undefined`,`bigInt`,`symbol`
- 对象类型
	-  `Object`

### 变量和作用域

- 变量声明 
	- `var`、`let`、`const`
- 作用域 - 定义变量和函数的可访问性
	- 全局作用域
		- 定义在最外层的变量，在任何地方都可访问
	- 局部作用域
		- 函数内部定义的变量
		- `{}` 内使用`let`、`const`声明的变量
- 变量提升
	- 涉及JS引擎相关知识
	- `var` - 在声明之前引用值是`undefined`
	- `function` - 被提升值顶部，即使是在声明之前也可以正常使用
	- `let`、`const` 
		- 暂时性死区 - 在声明之前引用会报错`ReferenceError`（引用错误）
	- 严格模式 - 严格模式下，变量没有声明之前不能被使用（函数除外？）
- 闭包
	- 当一个函数在另一个函数内被定义，内部函数访问了内部函数的变量，并且产生了引用（比如，将内部变量暴露出来）
### 类型转换

- 显式转换
	- `string` - `String()`、`.toString()`、
	- `number` - `Number()`、`+<变量>`
	- `boolean` - `Boolean()`、`!!<变量>`
- 隐式转换
	- 比较运算、算术运算
- 强制类型转换
	- 隐式转换子集
	- 转字符串：`number` + `string`，会被转换为字符串
	- 转布尔值：逻辑运算，`&&`、`||`、`三元运算`、`if`
- 特殊转换
	- `number`
		- `null=>0`
		- `undefined=>NaN`
		- `''=>0`
		- `' '=>NaN`
		- `true=>1`
		- `false=>0`
		- `[]=>0`
		- `[100]=>100`
		- `[1]=>NaN`
		- `{}=>NaN`

### 函数

- 生成函数
	- 函数声明 
		- `function` 关键字声明的函数
		- 存在变量提升
	- 函数表达式
		- 将函数赋值给变量
		- 定义之后才可以使用
	- 箭头函数
		- 更简洁
		- `this`是定义环境的this
		- 没有`arguments`
		- 不能作为构造函数
		- 没有`prototype`
- arguments
- `.name` - 函数名字
- `.length` - 函数参数长度

## 对象和原型

对象创建

- 字面量方法 - `const obj={}`
- 构造函数 - 使用`new`创建的对象
- `Object.create()` - 基于现有对象的原型创建新对象

原型和原型链

- 原型
	- 继承和共享属性的内部对象
- 原型链
	- 访问一个对象属性，若没有，则查找`__proto__`属性指向的对象，直到`__proto__`指向`null`，也就是原型链的顶端
- `prototype`
	- 函数都有该属性(除了箭头函数)
	- 通过该函数创造的对象的属性`__proto__`指向该函数的`protoytype`属性

### 循环/迭代

- `for`,`while`,`do while`,`break`,`continue`,`label`
- `for in` - 针对`Object`,迭代除了`symbol`以外的可枚举属性，包括继承的可枚举。
- `for of` - 针对可迭代对象
	- 可迭代对象是定义了`[Symbol.iterator]`
	- 比如`Array`,`Map`,`Set`,`String`,`Arguments`
- `for await of` - 仅用于异步可迭代的异步迭代器

### 模块化

- `import`,`export`
- 动态倒入-`import()`

---
## 异步编程

- 回调函数
- promise
	- `.then`,`.catch`,`.finally`
	- 常用静态方法
		- `.all` - 按照顺序返回，如果有一个被拒绝，则被拒绝
		- `.allSettled` - 不管成功与否，只要所有都执行完就返回
		- `.any` - 总返回第一个成功的，或者全部失败
		- `.rece` - 总返回率先完成的，不管成功与否
		- `.resolve`
		- `.reject`
- async/await
	- 顶层`await`-在ES6 模块顶层可直接使用
- `Generator` - `function *fn(){yield}`
- 事件循环


-----
## 函数和执行上下文

### 函数声明

### 执行上下文

执行上下文是指代码执行时的环境，决定了函数运行时的作用域链、变量、`this`

- 分类
	- 全局执行上下文
	- 函数执行上下文
	- `eval`执行上下文
### 函数调用

函数调用通常分为以下几个步骤完成

- 创建执行上下文
	- 变量环境 - 函数声明和局部变量
	- 词法环境 - 变量、函数、参数
	- 作用域链 
	- `this`绑定 -调用函数的对象引用
- 压入执行栈
- 初始化阶段 - 变量提升、创建作用域链
- 确定`this`的值
- 执行函数代码
- 弹出执行栈

特殊情况的执行上下文

- 箭头函数 - 没有`this`
- 全局执行上下文 - js程序一开始就创建了
- 递归调用 - 递归函数每次调用自己都会创建一个新的执行上下文
- 闭包 - 词法作用域被访问

- 调用堆栈
- 函数作用域，词法作用域
- 闭包
### this

- globalThis
- `this` 指向
	- 直接调用 `=>` `window`
	- 对象调用 `=>` 谁调用就指向谁
	- `new` `=>` 指向新生成的对象
- 改变`this`指向
	- `apply/call/bind` - `[],...[],...[]`

### 其他

- 递归
- 尾调用优化
- IIFE
- debounce
- throttle

---

其他
- 垃圾回收

 TODO 今天必刷
 https://github.com/stephentian/33-js-concepts

## 高级编程思想

元编程

- 概念
	- 编写能够操作代码的代码
	- 能够读取，生成，分析或变化其他程序的代码
- 实现
	- `Reflect API`
	- `Proxy`
	- `eval()`
	- `Function`
- 应用场景
	- 动态功能创建 - 根据情况不同，创建不同的函数或对象
	- 数据绑定和观察 - 响应式编程
	- API钩子和拦截 - 添加额外行为
	- 测试和模拟 - 测试

> 反射在元编程中的应用


## 对象描述符

对象属性管理，安全性和内存管理起到重要作用

- Object.defineProperty - 精确的添加或修改对象上的属性；
	- 数据描述符
	- 访问器描述符
	- 以上两种二选一，不能共存
- 描述符属性
	- `configurable`
		- 属性是否可配置，默认`false`
		- `false`
			- 无法删除
			- 不能再次修改`configurable`
			- 不能修改`enumerable`
			- 不能修改`writable`
			- 不能修改`value`
			- 可以修改`get`和`set`方法
		- `true`
			- 还可以再次编辑修改
- 数据描述符
	- `enumerable` - 是否可枚举
		- 默认`false`
	- `value` - 属性的值
		- 默认`undefined`
	- `writable` - 属性值是否可改写
		- 默认`false`
- 访问器描述符
	- `get`
	- `set`
- `Object.getOwnPropertyDescriptor()` - 返回自有属性的描述符
> 注意：使用`Object.defineProperty`定义对象描述符时，也会配置对象原型上的属性，可以考虑使用`Object.create(null)`避免修改原型，或者临时对象字面量也行。

### 属性的可枚举和所有权

`enumerable` 设置为 true的属性
- `in` - 包含继承所有
- `for...in` - 包含继承可枚举
- 返回属性
	- `Object.keys` - 自有可枚举
	- `getOwnPropertyNames` - 自有所有
	- `getOwnPropertySymbols` - 自有所有
- `Object.hasOwnProperty()` - 是否时自有属性
- `Object.propertyIsEnumberable()` - 是否是自有的可枚举属性

## Proxy

创建对象的代理，实现拦截等操作。

## Reflect

与`proxy`类似，但`Reflect`的所有属性都只是静态方法


---
## class 和 原型继承
