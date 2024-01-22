
Less、Sass，大概率用不了了。
## postcss


## 编辑器配置

- [VS Code 插件](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)
- [Prettier 排序](https://tailwindcss.com/blog/automatic-class-sorting-with-prettier#how-classes-are-sorted)

## postcss 预处理

依赖

```bash
npm install -D postcss-import autoprefixer postcss-nesting
```

配置

```js
// postcss.config.js
module.exports = {
  plugins: {
    'postcss-import': {}, // css 文件分块
    'tailwindcss/nesting': 'postcss-nesting', // css 嵌套
    tailwindcss: {},
    require('autoprefixer'), // 浏览器前缀
    ...(process.env.NODE_ENV === 'production' ? { cssnano: {} } : {}) // 压缩
  }
}
```

## 核心

- 伪类
- 响应式
- 深色模式

## 指令

- `@tailwind`
	- `base` - 原生元素样式，通常是重置css默认样式
	- `components` - 组件类名
	- `utilities` - 布局、文本、背景边框、响应式等类名
	- `variants` - 变体，伪类等
- `@layer`
- `@apply` - 在css中使用tailwind
- `theme()` - 使用tailwind变量
- `screen` - 媒体查询

## js 中访问 tailwind

[参考](https://tailwindcss.com/docs/configuration#referencing-in-java-script)

```js
import resolveConfig from 'tailwindcss/resolveConfig'
import tailwindConfig from './tailwind.config.js'

const fullConfig = resolveConfig(tailwindConfig)

fullConfig.theme.width[4]
// => '1rem'

fullConfig.theme.screens.md
// => '768px'

fullConfig.theme.boxShadow['2xl']
// => '0 25px 50px -12px rgba(0, 0, 0, 0.25)'
```