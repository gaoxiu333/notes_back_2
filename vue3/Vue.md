## Vue 组合式API

## 单文件组件

每个`*.vue`文件都由三种顶层语言模块构成`<template>`，`<script>`，`<style>`

- **`<template>`:**

  - `Fragment`: 碎片化节点， `template` 中只允许有多个根节点（Vue2只允许一个根节点）。

  - 文本插值：`<span>Message: {{ msg }}</span>`

  - 指令：

    - `v-bind`: 【缩写`:` 或者 `.` (当使用 `.prop` 修饰符)】动态的绑定一个或多个 attribute，也可以是组件的 prop。
    - `v-on`:【缩写`@`】给元素绑定事件监听器。

  - 内置特殊元素

    - `<component>`: 用于渲染动态组件的"元组件";要实际渲染的实际组件由`is`决定。
    - `<slot>`: 表示模板中的插槽内容出口。
    - `<template>`: 
      1. 用在单文件组件的顶层;
      2. 作为占位符，使用`v-if`、`v-for`、`v-solt`等指令（因为同一个元素只能使用一个指令）。

  - 内置Attributes

    - `key`:比较新旧节点列表时用于识别 vnode；当`key`变更时会强制替换元素，并不会复用（Vue进行了优化，渲染时通常会尽可能的复用相同类型的元素）。

      - 触发组件声明周期
      - 触发过渡动画

    - `ref`： 用于注册元素或子组件的引用。

    - `is`:  用于绑定动态组件，可以使用`vue:`前缀绑替换原生组件。

      ```html
      <!-- my-row-component 自定义组件会将 tr元素替换掉 -->
      <table>
        <tr is="vue:my-row-component"></tr>
      </table>
      ```

- **`<script>`:**

  - `<script setup>`：为什么要用`<script setup>`?
    - 更少的样板内容，更简洁的代码。
    - 能够使用纯 TypeScript 声明 props 和自定义事件。
    - 更好的运行时性能 (其模板会被编译成同一作用域内的渲染函数，避免了渲染上下文代理对象)。
    - 更好的 IDE 类型推导性能 (减少了语言服务器从代码中抽取类型的工作)。
  - `defineProps`: 用来声明`props`
  - `defineEmits`：用来声明`emits`
  - `defineExpose`：组件中要暴露出去的属性和方法，父组件通过模版引用访问暴露出来的属性和方法。

- **`<style>`:**

  - `scoped`: 使用 `scoped` 后，父组件的样式将不会渗透到子组件中；
  - 有三个伪类以应对不同的场景：
    - `:deep()`: 穿透影响子组件样式，在父组件中修改子组件样式时很有用；
    - `:slotted()`:插槽选择器，明确地将插槽内容作为选择器的目标，修改插槽内元素的样式；
    - `:global()`: 全局选择器，在`scoped`内定义全局样式，不受作用域影响。
  - `v-bind()`：支持在style中动态绑定
  
  ```vue
  <script setup>
  const theme = reactive({
    color: 'red'
  })
  </script>
  <style scoped>
  p {
    color: v-bind('theme.color');   /*  v-bind 绑定  */
  }
    /* 全局  */
  :global(.red) {}
    /* 插槽 */
  :slotted(div) {}
   /* 深度选择器 */
  .a :deep(.b) {}
  </style>
  ```

## 生命周期

- Vue3.0中可以继续使用Vue2.x中的生命周期钩子，但有有两个被更名：
  - `beforeDestroy`改名为 `beforeUnmount`
  - `destroyed`改名为 `unmounted`
  
- Vue3.0也提供了 Composition API 形式的生命周期钩子，与Vue2.x中钩子对应关系如下（部分）：
  - `beforeCreate`======>`setup()`
  - `created`==========>`setup()`
  - `beforeMount` ======>`onBeforeMount`
  - `mounted`==========>`onMounted`
  - `beforeUpdate`======>`onBeforeUpdate`
  - `updated` ==========>`onUpdated`
  - `beforeUnmount` ====>`onBeforeUnmount`
  - `unmounted` ========>`onUnmounted`
  - `errorCaptured` ====> `onErrorCaptured`
  
  > **注意：**setup比beforeCreate还早。

## setup

`setup()` 钩子是在组件中使用组合式 API 的入口。

- setup是一个函数
- 组件的数据、方法、生命周期等均在setup函数中配置。
- setup有两种返回值：
  1. `return`一个对象，对象属性会暴露给模板和其他的选项式 API 钩子
  2. `return`一个渲染函数，此渲染函数会代替`<template>`模版。
- setup有两个参数：
  1. 参数一：`props`组件的传值
  2. 参数二：`context`执行上下文，类似选项式组件中的`this`

## `<script setup>`

#### 为什么要用`<script setup>`?

- 更少的样板内容，更简洁的代码。
- 能够使用纯 TypeScript 声明 props 和自定义事件。
- 更好的运行时性能 (其模板会被编译成同一作用域内的渲染函数，避免了渲染上下文代理对象)。
- 更好的 IDE 类型推导性能 (减少了语言服务器从代码中抽取类型的工作)。

#### 定义响应式数据

- `ref()`
  - 接受基本类型，也可以是引用类型；返回响应式数据的引用对象（reference对象，简称ref对象）；
  - 基本类型基于`defineProperty`原理，内部源码用的是class的get和set;
  - 引用类型在内部借用`reactive()`；
  - 使用时通过`.value`访问响应式数据；
- `reactive()`
  - 只接受对象，返回一个对象的响应式代理（proxy对象）；
  - reactive定义的响应式数据是“深层次的”，嵌套属性同样是响应式的；
  - 内部基于 ES6 的 Proxy 实现，通过代理对象操作源对象内部数据进行操作；
- `reactive`对比`ref`
  - 从定义数据角度对比：
    - ref用来定义：**基本类型数据**。
    - reactive用来定义：**对象（或数组）类型数据**。
    - 备注：ref也可以用来定义**对象（或数组）类型数据**, 它内部会自动通过`reactive`转为**代理对象**。
  - 从原理角度对比：
    - ref通过`Object.defineProperty()`的`get`与`set`来实现响应式（数据劫持）。
    - reactive通过使用**Proxy**来实现响应式（数据劫持）, 并通过**Reflect**操作**源对象**内部的数据。
  - 从使用角度对比：
    - ref定义的数据：操作数据**需要**`.value`，**可以重新赋值**，重新赋之后依然保持响应。
    - reactive定义的数据：操作数据与读取数据：**均不需要**`.value`；**不能重新赋值**，只能修改属性。


### 组件



