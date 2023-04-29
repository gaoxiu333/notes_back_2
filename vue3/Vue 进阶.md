# 全局API

支持ES模块，按需引入。

```js
import { createApp, h, nextTick } from 'vue'
```

## createApp

创建一个应用实例。

```js
import { createApp } from 'vue'

const app = createApp({})
```

Vu2中很多全局API挂载到了应用程序实例下面；比如：

- `component`
- `directive`
- `mixin`
- `provide`&`inject`
- `use`
- `mount`
- `unmount`
- `version`

### 应用程序配置

每个 Vue 应用程序都会公开一个对象`config`，其中包含该应用程序的配置设置：

```js
const app = createApp({})

console.log(app.config)
```

**配置全局属性**

```js
// Vue2 写法
Vue.prototype.$http = () => {}

// Vue3 写法
const app = createApp({})
app.config.globalProperties.$http = () => {}
// 被所有组件实例继承
app.component('child-component', {
  mounted() {
    console.log(this.foo) // 'bar'
  }
})
```

**其他配置**

- `errorHandler`
- `warnHandler`
- `compilerOptions`
- `globalProperties`
- `optionMergeStrategies`

## h()

渲染函数，创建虚拟 DOM 节点 (vnode)。

**参数**：

它需要三个参数：`type`，`props`和`children`

创建原生元素

- 创建组件

  ```js
  import { h } from 'vue'
  
  // 除了 type 外，其他参数都是可选的
  h('div')
  h('div', { id: 'foo' })
  // 没有 prop 时可以省略不写
  h('div', 'hello')
  h('div', [h('span', 'hello')])
  ```

- 创建组件

  ```js
  import Foo from './Foo.vue'
  
  // 传递 prop
  h(Foo, {
    someProp: 'hello',   // 等价于 some-prop="hello"
    onUpdate: () => {}   // 等价于 @update="() => {}"
  })
  
  // 传递单个默认插槽
  h(Foo, () => 'default slot')
  
  // 传递具名插槽
  // 注意，需要使用 `null` 来避免
  // 插槽对象被当作是 prop
  h(MyComponent, null, {
    default: () => 'default slot',
    foo: () => h('div', 'foo'),
    bar: () => [h('span', 'one'), h('span', 'two')]
  })
  ```

## nextTick()

等待下一次 DOM 更新刷新的工具方法。

```js
import { createApp, nextTick } from 'vue'

const app = createApp({
  setup() {
    const message = ref('msg!')
    const changeMessage = async newMessage => {
      message.value = 'is new message!'
      await nextTick()
      console.log('DOM 已完成更新！')
    }
  }
})
```

## mergeProps()

合并多个 props 对象，后面的同名属性优先；以下三个有特定的合并方式：

- `class` or `style` - 属性的值将被连接起来而不是被覆盖；
- `onXxx` - 事件监听器会被合并到一个数组中，也不会被覆盖。

```js
import { h, mergeProps } from 'vue'

export default {
  inheritAttrs: false,

  render() {
    const props = mergeProps(
      {
        // 将自定义的prop和this.$attrs合并
        class: 'active'
      },
      this.$attrs
    )
    return h('div', props)
  }
}
```

