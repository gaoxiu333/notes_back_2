# state

相关面试题：

- 说说 React 中的 State
- 为什么 React 推荐组件的状态是不可变对象？
- 为什么不能直接通过 `this.state` 直接修改状态？

#### 组件中的哪些属性或者变量可以是 State？

1. 是否是通过 `props` 父组件获取 
2. 是否在整个生命周期中保持不变
3. 是否可以通过现在变量计算所得
4. 是否在组件 `render()`  中使用

#### Immutable 不可变对象

官方建议把 State 当作是不可变对象，当 State 中的某个状态发生变化，应该重新创建状态对象，而不是直接修改。

根据状态类型分为三种数据类型：

- 基本数据类型
- 数组类型
  - 不能使用数组突变方法，如：`push()`、`pop()`、`shift()`、`unshift()`、`splice()`
  - 使用`slice()`、`filter()`、`concat()`和拓展元算符等生成新数组
- 对象类型
  - 使用 `Object.assign()` 或 拓展运算符

> 创建新的状态对象的关键是，避免使用会**直接修改**原对象的方法，而是使用可以**返回一个新对象**的方法。当然，也可以使用一些不可变对象的 JavaScript 库，如 [Immutable.js](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Ffacebook%2Fimmutable-js)。

**为什么 React 推荐组件的状态是不可变对象？**

- 不可变对象方便管理和调试
- 出于性能考虑，在组件更新时能减少比较次数，提高性能
  - 手段：
  - `shouldComponentUpdate` 声明周期
  - `PureComponent` 组件

为什么不可变对象会快？

- 可以使用浅层相等比较
- 检查两个不同的*变量*是否引用同一个对象；相反，深度相等性检查（或*值相等性*）必须检查两个对象属性的每个*值。*

## setState

为了提高框架性能，React 将 `setState` 设置为 **状态批量处理或推迟更新**，实际上就是 **异步操作函数**，该方法不会以顺序控制流的方式处理相同周期内的事件.

- 直接修改 `state` 不会触发组件重新渲染
- 不是单纯的异步或同步，这其实与调用时的环境相关。
  - 异步：合成事件和生命周期中
  - 同步：浏览器原生事件或`setTimeout`
- 批量更新
  - `setState` 合并，在合成事件和生命周期函数中多次连续调用会被优化为一次；
