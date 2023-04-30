# 响应式API

选项式 API 会用 `data` 选项来声明组件的响应式状态；

组合式 API 需要用到`reactive()`、`ref()`等函数创建响应式数据。

## `reactive()`

创建一个响应式对象或数组。

**描述：**

- 基于`ES6 Proxy`实现，对响应数据对象属性的访问与更改操作。
- 默认创建深层响应式数据，会影响所有嵌套的属性。

```js
import { reactive } from 'vue'

const state = reactive({ count: 0 })
```

**局限性：**

- 仅对对象类型有效，对基础类型无效；
- 需要保持引用，不能重新被赋值；
- 响应式对象属性不能赋值给本地变量，会失去响应式：

```js
const state = reactive({ count: 0 })

// 失去响应性连接
let n = state.count

// count 也和 state.count 失去了响应性连接
let { count } = state

// state.count 赋值给函数参数，失去响应
callSomeFunction(state.count)
```

## `ref()`

创建可以使用任何值类型的响应式数据。

**描述：**

- 返回的响应式数据会包装在`.value`属性里
- **基本类型**使用`defineProperty`劫持，实现响应式数据
- **引用类型**内部调用`reactive`转换为响应式数据

```js
const count = ref(0)

console.log(count) // { value: 0 }
console.log(count.value) // 0

count.value++
console.log(count.value) // 1
```

**.value解包**

`ref()`创建的响应式数据，需要访问`.value`属性，有以下几个场景会自动解包，不需要`.value`

- 在`<template>`模版作为顶层属性时；
- 在`<template>`模版中不是顶层属性：
  - 在文本插值语法中（即一个 `{{ }}` 符号）
  - 在`JavaScript`表达式中**不会解包**
- 在响应式对象中，作为响应式对象的一个属性值时，并且相互关联
  - 数组和`Map`类型的对象除外

在`<template>`中

```vue
<script setup>
import { ref } from 'vue'

const count = ref(0)
const object = { foo: ref(1) }

function increment() {
  count.value++
}
</script>

<template>
  <button @click="increment">
    {{ count }} <!--【自动解包】 无需 .value -->
  </button>
	<span>{{ object.foo }}</span><!--【自动解包】 -->
	<span>{{ object.foo + 1 }}</span><!--【不能自动解包】 -->
</template>

```

作为响应式对象属性

```js
const count = ref(0)
const state = reactive({
  count
})
//【自动解包】 无需 .value
console.log(state.count) // 0 

state.count = 1
console.log(count.value) // 1

const books = reactive([ref('Vue 3 Guide')])
//【不能自动解包】 这里需要 .value
console.log(books[0].value)

```

## `ref()` VS `reactive()`

ref既然可以创建所有类型的影响式数据，为什么还有reactive？

- `reactive()`访问属性时，不需要`.value`
- `reactive()`适合将一组相关联的状态集合，避免`.value`造成的心智负担
- `ref()`更加灵活，可以定所有类型的响应式数据

结合以上几点，到底该如何取舍，我觉得取决于编程习惯。

## `computed()`

接收一个`getter`函数，并且返回一个响应式 ref 对象

- 和`ref`创建的响应式数据一样，通过`.value`访问响应式数据
- 只有当`getter`函数内的响应式依赖更新时，计算属性才会重新执行；

创建一个只读计算属性：

```js
const count = ref(1)
const plusOne = computed(() => count.value + 1)

console.log(plusOne.value) // 2

plusOne.value++ // 错误

```

创建一个可写的计算属性：

```js
const count = ref(1)
const plusOne = computed({
  get: () => count.value + 1,
  set: (val) => {
    count.value = val - 1
  },
  onTrack(e) {
    // 被追踪为依赖时触发（访问读取时）
  },
  onTrigger(e) {
    // 当被更改时触发（修改时）
  }
})

plusOne.value = 1
console.log(count.value) // 0
```

## `watch()`

