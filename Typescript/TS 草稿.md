# TypeScript

*TypeScript* - *TS* ，是一种由微软开发的自由和开源的编程语言。

随着项目规模的增大，原始弱类型 JavaScript 已不能满足需求。因此类型安全的 Typescript 应运而生。它是 JS 的超集，大大提高了代码的可读性和可维护性；同时，它可与原 JS 共存，项目可通过渐进式迁移至新项目。

### TypeScript 是什么

*TypeScript* 是 *JavaScript* 的 **超集** ，简单的说就是在 *JavaScript* 的基础上加入了 **类型系统**，让每个参数都有明确的意义，从而带来了更加 **智能** 的提示。

*TypeScript* 属于**强类型**语言，所以对于项目而言，会使代码更加规范，从而解决了大型项目代码的复杂性。

## 资料

#### 官方资料

- [TypeScript Playground](https://www.typescriptlang.org/play)：在线调试
  - [Babel](https://babeljs.io/repl#?presets=typescript)：Babel 的在线调试
- [TSConfig](https://www.typescriptlang.org/tsconfig)：config配置说明
- [tsc CLI](https://www.typescriptlang.org/docs/handbook/compiler-options.html)：命令行

- [cheat sheets](https://www.typescriptlang.org/cheatsheets)：语法速记
  - [语法速查](https://learnxinyminutes.com/docs/typescript/) - 非官方

- [Do's and Don'ts](https://www.typescriptlang.org/docs/handbook/declaration-files/do-s-and-don-ts.html)：最佳实践小例子

#### 社区教程

- [傅说 | 玩转 TypeScript](https://mp.weixin.qq.com/s/9OZMfsUagYr96fD5uNsoiA)
- [TypeScript 入门指南](https://rualc.com/cs/typescript-language-basic/#gai-lan-2)
- [官方手册汉化](https://github.com/zhongsp/TypeScript)
- [TypeScript 入门教程](https://ts.xcatliu.com/)
- [深入理解 TypeScript](https://jkchao.github.io/typescript-book-chinese/)
- [TS 常见问题](https://juejin.cn/post/6844904055039344654)
- 

## TypeScript 环境

- 运行
  - [命令行](https://www.typescriptlang.org/docs/handbook/compiler-options.html) - `tsc`
  - [parcel](https://parceljs.org/) - 快速构建一个 TS 运行环境
- 运行配置
  - [Compiler Options](https://www.typescriptlang.org/docs/handbook/compiler-options.html)：编译选项
  - [tsconfig.json](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)：配置文件

- 工程化
  - 工具
    - [types-checker](https://www.npmjs.com/package/types-checker)：自动安装 @types
    - [DefinitelyTyped](http://definitelytyped.org/)：@types 官网

  - ESLint
    - [Getting Started with ESLint ](https://eslint.org/docs/user-guide/getting-started)：ESLint 官方教程
    - [@typescript-eslint/parser](https://github.com/typescript-eslint/typescript-eslint/tree/master/packages/parser)：ESLint 的 TS 插件

  - 打包插件
    - [@babel/preset-typescript ](https://babeljs.io/docs/en/babel-preset-typescript)：babel 的
    - [rollup-plugin-typescript2 ](https://www.npmjs.com/package/rollup-plugin-typescript2)：rollup 


## TypeScript 基础语法

#### 安装&使用

```bash
npm init -y #初始化项目
npm i typescript # 安装 TS
npx tsc --init # 初始化 TS 项目，生成TSConfig.json
npm init @eslint/config # 初始化 ESlint 配置
```

## 类型

- 基本类型
  - *string*, *number*, *boolean*, *symbol*, *bigint*, *null*, *undefined*
- 引用类型
  - *array*,  *Tuple*元组,  *object*包含*Object*和*{}*, *function*
- 特殊类型
  - *any*, *unknow*, *void*, *nerver*, *enum*
- 别名/接口
  - *type*, *interface*
- 其他类型
  - 类型推理、字面量类型、交叉类型

### 基本类型

```typescript
//字符串
let str: string = "Domes";

// 数字
let num: number = 7;

//布尔
let bool: boolean = true;

//symbol
let sym: symbol;
// TS2585: 'Symbol' only refers to a type, but is being used as a value here. Do you need to change your target library? Try changing the 'lib' compiler option to es2015 or later.


//bigint
let big: bigint = 10n;
// TS2737: BigInt literals are not available when targeting lower than ES2020

//null
let nu: null = null;

//undefined
let un: undefined = undefined;
```

> Note:
>
> - *null* 和 *undefined* 两个类型一旦赋值上，就不能在赋值给任何其他类型

### 引用类型

#### Array 数组

两种使用方式：

1. T + `[]`
2. `Array<T>`：泛型语法

```typescript
let arr1: number[] = [1, 2, 3]

let arr2: Array<number> = [1, 2, 3]

let arr3: Array<number> = [1, 2, '3'] // error
// TS2322: Type 'string' is not assignable to type 'number'.

// 支持多种类型，使用｜符号
let arr4: Array<number | string> = [1, 2, '3'] //ok
```

#### Tuple 元祖

*Tuple* 可以说是 *Array* 的一种特殊情况。

-  *Tuple* 的作用就是限制 **元素的类型** 并且 **限制个数** 的数组
- 可以使用 `push` 等操作元祖，但是修改后长度不能通过下标访问
- *TS 4.0* 后支持标签

```typescript
let t: [number, string] = [1, '2']; // ok
```

#### Object 对象

- object：**首字母小写**几乎不用，常用`{}`
- Object：**首字母大写**表示`Object`实例，除了`null`、`undefined`的所有类型

```typescript
let obj1: object = {a: 1, b: 2}
obj1.a = 3 // error
let obj: Object;
obj = null; // error
// Type 'null' is not assignable to type 'Object'.(2322)
obj = undefined; // error
// Type 'undefined' is not assignable to type 'Object'.(2322)
```

#### 函数

```
JavaScript --> TypeScript
  
  class TypeScript{
    含有类型
    箭头函数
    函数类型
    必填和可选参数
    默认参数
    剩余参数
    函数重载
  }
     
  class JavaScript{
    无类型
    箭头函数（ES2015）
    无函数类型
    所有参数都是可选的
    默认参数
    剩余参数
    无函数重载
  }
```

- 定义函数

  - `function`

  - 箭头函数

- 函数重载
  - 使用 **相同名称** 和 **不同参数数量或类型** 创建多个方法的一种能力
  - 引擎按照自上而下的顺序查找重载表，因此要把最精确的定义放在最前面，以减少查找时间。
- 返回值类型
  - 没有定义时，TS会根据类型推断设置返回值类型

### 特殊类型

- any
  - 任何类型都可以归于 *any* 类型
  - 如果不设置类型，并且不进行赋值时，将会被被自动推论为 *any* 类型
- unknow
  - *unknow* 与 *any* 一样，都可以作为所有类型的 **顶级类型** ，但 *unknow* 更加**严格**
  - 只能被赋值给 *any* 类型和 *unknown* 类型本身
- void
  - 当一个函数，没有返回值时，*TS* 会默认它的返回值为 *void* 类型，实际为 *undefined* 
- never
  - *never* 表示一个函数永远不存在返回值
  - 与 *void* 相比， *never* 应该是 *void* 子集， 因为 *void* 实际上的返回值为 *undefined* ，而 *never* 连 *undefined* 也不行
  - 符合 *never* 的情况有：当抛出异常的情况和无限死循环
- enum 枚举
  - 可以定义一些带名字的常量
  - 枚举的类型只能是 *string* 或 *number*
  - 定义的名称不能为 **关键字**

