### 内置hook

- useState
- useReducer
- useContext
- useEffect



### 创建共享数据的 Hook

- 创建hooks注意：必须遵循 React  的命名规范，有一个有效的 Hooks 里面应该是调用了其他的Hooks，比如 React 内置的 Hooks。



特点：

- Custom Hooks 只共享状态逻辑，而不是状态本身。
- 每次您的组件重新渲染时，所有 Hooks 都会重新运行。
- 将自定义 Hook 接收到的事件处理程序包装到 Effect Events 中。
- 可以接受 响应式数据，根据响应式数据变化处理相同的事情
- 可以接受 事件处理程序，