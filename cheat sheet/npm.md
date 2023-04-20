# NPM Cheat Sheet

npm 备忘单

### 查看版本

```bash
npm -v
npm --version
```

### 获取帮助

```bash
npm
npm help
```

### npm配置

```bash
npm config set <key>=<value>  # 设置某个配置
npm config get <key>          # 查看某个配置
npm config list               # 查看配置列表
npm config ls -l              # 查看npm所有默认配置
npm config delete <key>       # 删除配置
npm config edit               # 编辑配置
npm config fix                # 自动修复错误或者无效的配置
```

### 创建`package.json`

```bash
npm init
npm init -y 	# 创建package.json，并且使用默认配置
npm init --yes
```

### 安装包

```bash
# 中括号内为别名
npm i                               # npm@5之后，默认和 --save 一样
npm i --save package-name           # [-S,-P] 安装在 dependencies，这是默认设置     
npm i --save-dev package-name       # [-D] 安装在 devDependencies
npm i --save-optional package-name  # [-O] 安装在 optionalDependencies
npm i --no-save package-name        # 防止保存到dependencies
npm i --save-exact package-name     # [-E]安装一个确切版本的包
npm i --save-bundle package-name    # [-B] 安装在 bundleDependencies
npm i -g package-name               # 全局安装
npm i --production                  # 安装除了 devDependecies 之外的所有内容
```

> npm i
>
> TODO 版本 ^ ~

### 安装包名称（版本）

```bash
```



### 更新包

```bash
npm update -g package-name
npm update --save package-name
npm update --save-dev package-name
```

### 删除包

```bash
npm uninstall -g package-name
npm uninstall -save package-name
npm uninstall --save-dev package-name
```

### 查看包

```bash
# 查看全局
npm list -g # 别名 npm ls
npm list -g --depth 0
npm list -g --depth 1
# 查看本地
npm list 
npm list --depth 0
npm list --depth 1
# 检查过时的依赖包
npm outdated
```

### npm脚本

TODO：script脚本支持bash语言？更深入了解需要学习？

```json
// package.json中设置scripts属性
"scripts":{
  "start":"node index.js",
  "script-name":"command-to-run"
}
# 运行
npm start // start可以省去run命令
npm run script-name
```

### 包版本

`*`，`~`，`^`

- `*`：安装最新版本的包
- `~`：安装具有最新补丁更新的如那件包
- `^`：使用最新的次要更新安装包

### npm 发布

```bash
npm version # 版本管理
```





## TODO

npm node_modules的层级关系

- 常见问题处理

- # npm cache clean --force

  - z

参考：

- [npm audit](http://eux.baidu.com/blog/fe/npm%20aduit%E4%BA%8C%E4%B8%89%E4%BA%8B)