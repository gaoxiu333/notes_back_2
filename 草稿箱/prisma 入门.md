
## 安装

如果需要实用`ts`来写，需要安装`typescript`支持
```bash
npm install prisma typescript ts-node @types/node --save-dev
```
接下来需要初始化
```bash
npx tsc --init # 初始化ts
npx prisma init --datasource-provider sqlite # 使用SQLite数据库初始化
```

## 建模

设置数据模型

## 迁移数据

```bash
npx prisma migrate dev --name init
```

该命令做了三件事：
1. 创建`prisma/migrations`
2. 执行 SQL 迁移文件
3. 没懂

----
1. 主键问题，主键应该是ID么？
	1. 主键设计如何查找？
	2. 查找是基于什么去查找？
	3. 如果已知的信息不是主键，那么查找就设计二次查找了。


---
PRC - 无API设计

## 常用命令

显示数据库UI

```bash
npx prisma studio
```

- 删除表/重置表
	- ``