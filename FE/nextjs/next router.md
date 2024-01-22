
目录结构

```bash
.
├── README.md
├── api
├── app
│   ├── about
│   │   └── page.tsx
│   ├── layout.tsx 
│   └── page.tsx # 1. 根路由
├── components
├── lib
├── next-env.d.ts
├── next.config.js
├── package-lock.json
├── package.json
├── pnpm-lock.yaml
├── postcss.config.js
├── public
│   ├── favicon.png
│   ├── favicon.svg
│   ├── next.svg
│   └── vercel.svg
├── styles
│   └── globals.css
├── tailwind.config.ts
├── tsconfig.json
└── yarn-error.log
```


## 路由

- page 被视为路由的有效路径，没有page文件，被视为无效路由
- `_page` - 下划线开头的文件被无视
## 根路由

跟路由可以配置多个，配置方法可参考官方文档[Creating multiple root layouts](https://nextjs.org/docs/app/building-your-application/routing/route-groups#creating-multiple-root-layouts)

- `page`
- `lyaout`
	- 可修改网站元数据
	- `<head/>` 
	- favicon 
- template
- loading
- error
> TODO: template 和 layout 在渲染上有什么区别？以及page和components？
