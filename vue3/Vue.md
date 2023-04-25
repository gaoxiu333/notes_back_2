## Vue 组合式API

### setup()







### 单文件组件

每个`*.vue`文件都由三种顶层语言模块构成`<template>`，`<script>`，`<style>`

- `<template>`:

  - **文本插值**：`<span>Message: {{ msg }}</span>`

  - **指令：**

    - `v-bind`: 动态的绑定一个或多个 attribute，也可以是组件的 prop。
      - **缩写：**`:` 或者 `.` (当使用 `.prop` 修饰符)
    - `v-on`:给元素绑定事件监听器。
      - **缩写：**`@`

  - **内置特殊元素**

    - `<component>`: 用于渲染动态组件的"元组件"。
      - 要实际渲染的实际组件由`is`决定。
    - `<slot>`: 表示模板中的插槽内容出口。
    - `<template>`: 用在单文件组件的顶层，或者作为占位符使用，可以使用`v-if`、`v-for`、`v-solt`等指令。

  - **内置Attributes**

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

- `<script>`:

  - `<script setup>`：为什么要用`<script setup>`?
    - 更少的样板内容，更简洁的代码。
    - 能够使用纯 TypeScript 声明 props 和自定义事件。
    - 更好的运行时性能 (其模板会被编译成同一作用域内的渲染函数，避免了渲染上下文代理对象)。
    - 更好的 IDE 类型推导性能 (减少了语言服务器从代码中抽取类型的工作)。
  - `defineProps`: 用来声明`props`
  - `defineEmits`：用来声明`emits`
  - `defineExpose`：组件中要暴露出去的属性和方法，父组件通过模版引用访问暴露出来的属性和方法。

- `<style>`:

  - `scoped`: 使用 `scoped` 后，父组件的样式将不会渗透到子组件中。
    - `:deep()`: 穿透影响子组件样式。
    - `:slotted()`:插槽选择器。
    - `:global()`: 全局选择器
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
  :global(.red) {
    color: red;
  }
    /* 插槽 */
  :slotted(div) {
    color: red;
  }
   /* 深度选择器 */
  .a :deep(.b) {
  
  }
  </style>
  ```

  



