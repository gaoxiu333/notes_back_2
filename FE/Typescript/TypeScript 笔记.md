

## 支持文件类型

### 支持JSON

`resolveJsonModule:true`
`"moduleResolution": "node"`

> 支持JSON 不仅需要开启`resolveJsonModule`，还需要`moduleResolution`配置为`node`，使用node模块解析策略。

### 支持js文件

`esModuleInterop:true` - 开启 CommonJS 模块的导入