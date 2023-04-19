# NPM Cheat Sheet

npm 备忘单

### 版本

```bash
npm -v
npm --version
```

### 帮助

```bash
npm
npm help
```

### 创建`package.json`

```bash
npm init
npm init -y 	# 创建package.json，并且使用默认配置
npm init --yes
```

### 安装包

```bash
npm i -g package-name					#全局安装
npm i --save package-name			#生产依赖
npm i --save-dev package-name	#开发依赖
npm i													#安装生产和开发依赖(production&development)
npm i --production						#仅安装生产依赖

```

### 更新包

```bash
npm update -g package-name
npm	update --save package-name
npm update --save-dev package-name
```

### 删除包

```bash
npm uninstall -g package-name
npm uninstall -save package-name
npm uninstall --save-dev package-name
```





### 其他

```bash
# 设置
npm config set init-author-name 'Your Name' # 设置 package.json 中作者的名字
npm config set init-author-email 'Your Email' # 设置 package.json 中作者的名字
npm config set init-license 'MIT'	# 设置 package.json 中许可，默认 ISC 
... 其他查看 npm config
# 查看
npm config get init-author-name
# 删除
npm config delete init-author-name
```

## TODO

npm node_modules的层级关系