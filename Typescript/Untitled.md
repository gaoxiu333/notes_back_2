# 傅说 | 玩转 TypeScript

原创 傅森广 [hello言值](javascript:void(0);) *2023-05-13 09:42* *发表于浙江*

> 随着项目规模的增大，原始弱类型 JavaScript 已不能满足需求。因此类型安全的 Typescript 应运而生。它是 JS 的超集，大大提高了代码的可读性和可维护性；同时，它可与原 JS 共存，项目可通过渐进式迁移至新项目。这里就随我一起揭开 TypeScript 的神秘面纱，一探究竟。

# Typescript

*TypeScript* - *TS* ，是一种由微软开发的自由和开源的编程语言。

```
flowchart LR

%%--level 1
0("Typescript")
1["TS是什么"]
2["TS的基本数据类型"]
3["Class"]
4["断言与类型守卫"]
5["范型"]
6["<ruby>联合类型<rt>Union Type</rt></ruby>"]
7["别名与接口"]
8["常用技巧"]
%%--level 0 relation
1---0;2---0;3---0;4---0;
0---5;0---6;0---7;0---8

subgraph &nbsp
%%--level 1
1.1["TS和JS的关系"]
1.2["安装TS"]
1.3["编译"]
%%--level 1 relation
1.1---1;1.2---1;1.3---1

%%--level 2
2.1["基本类型"]
2.2["引用类型"]
2.3["特殊类型"]
2.4["其它类型"]
%%--level 2 relation
2.1---2;2.2---2;2.3---2;2.4---2;

%%--level 3
3.1["基本方法"]
3.2["私有字段"]
3.3["只读属性"]
3.4["继承"]
3.5["修饰符"]
3.6["abstract"]
3.7["重写与重载"]
%%--level 3 relation
3.1---3;3.2---3;3.3---3;3.4---3;3.5---3;3.6---3;3.7---3;

%%--level 4
4.1["TS断言"]
4.2["类型守卫"]
%%--level 4 relation
4.1---4;4.2---4;
end

subgraph &nbsp&nbsp
%%--level 5
5.1["语法"]
5.2["多类型传参"]
5.3["接口"]
5.4["类"]
5.5["类别名"]
5.6["默认参数"]
5.7["常用字母"]
%%--level 5 relation
5---5.1;5---5.2;5---5.3;5---5.4;5---5.5;5---5.6;5---5.7

%%--level 6
6.1["可辨识联合"]
%%--level 6 relation
6---6.1

%%--level 7
7.1["类型别名"]
7.2["接口"]
7.3["type和interface区别"]
%%--level 7 relation
7---7.1;7---7.2;7---7.3

%%--level 8
8.1["extends"]
8.2["tepeof"]
8.3["keyof"]
8.4["索引访问操作符"]
8.5["in"]
8.6["infer"]
8.7["..."]
%%--level 8 relation
8---8.1;8---8.2;8---8.3;8---8.4;8---8.5;8---8.6;8---8.7
end

classDef transparent fill:none,stroke:none
class &nbsp,&nbsp&nbsp transparent
```

*TypeScript* 是 *JavaScript* 的 **超集** ，简单的说就是在 *JavaScript* 的基础上加入了 **类型系统***type system*，让每个参数都有明确的意义，从而带来了更加 **智能** 的提示。

*TypeScript* 属于**强类型**语言，所以对于项目而言，会使代码更加规范，从而解决了大型项目代码的复杂性。

*TypeScript* 可以分为两部份：

1. *EcmaScript* 的高阶语法糖

主要包括不同版本的 *JS* 相互兼容、*Class* 的 *implements* 实现接口继承、 *abstract* 实现抽象类、以及目前还停留在 *stage2* 的 *@decorator*编译时需添加 `--experimentalDecorators` 参数

——这部分通过 *Babel* 也可实现相同效果

1. 另一部分是强类型的类型系统，主要包括了 *Type*^类型^, *Assertion*^断言^, *Guards*^类型守卫^, *Interfaces*^接口^, *Generics*^泛型^。另外还有一些交叉知识

第一部分将会被自动转换，比如 *ES2022* 中的 *#* 编译为低版本时由 *WeakMap(this, privateKeys)* 实现；而第二部分不会被编译为 *JavaScript* ，在输入代码时进行动态类型检查。搞懂这两部分关系，学习就轻松多了。

对于一般的面向对象语言，继承有两种：接口继承*interface inheritance* 和 实现继承*implement inheritance* ，*ES* 只实现了后者，而 *TS* 通过 *interface* 关键字解决了这个问题 。另外 *TS* 又从 *C++, Haskell* 借鉴了一部分的语法。*TS* 弥补了大量不足，使得 *JS* 成为了一门强大的语言。

浏览器不能直接识别 *TypeScript* ，所以在编译的时候，*TypeScript* 文件会先编译为 *JavaScript* 文件。

```
graph LR
T-->|编译|J1
J1-->|打包|J2
J2-->|部署|C

T("TypeScript<tt><div style='border:1px dashed;padding:1em;margin:.5em'>a.ts<br>b.ts<br>c.ts</div></tt>")
J1("JavaScript<tt><div style='border:1px dashed;padding:1em;margin:.5em'>a.js<br>b.js<br>c.js</div></tt>")
J2("JavaScript<tt><div style='border:1px dashed;padding:1em;margin:.5em'><br>main.js<br><br></div></tt>")
C("Chrome<tt><div style='border:1px dashed;padding:1em;margin:.5em'><br>main.js<br><br></div></tt>")
```

## *Usage*^使用^

1. 安装

```
$ npm install -g typescript 
 //或
$ yarn global add typescript
// package.json
"devDependencies": {
  "typescript": "^4.7.4",
  "jslint": "^0.12.1"
}
```

然后运行 `(npm install) && (npx tsc --init)` 进行初始化。现在不需要单独安装 `tsc` 了。

1. 查看版本

```
$ tsc -v
```

1. 编译

```
$ tsc test.ts
# test.ts => test.js
// package.json
"scripts": {
  "start": "tsc && (node out/entry.js)",
  "init": "clear && (npm install) && (npx tsc --init) && (npm init @eslint/config)"
},
```

1. 参数

使用 `-t` 指定编译后的 *ES* 版本，使用 `-lib` 指定库

:memo: *Note*`-lib` 参数接受一个数组 *list* 。

可以在 Webstrom中指定单个 Typescript 文件的编译，参数设置如下：

```
$ -t ES2020 --lib: ["ES2020", "DOM"] --alwaysStrict test.ts
```

1. 在线编译

方便起见，可以使用线上的编辑器：***TypeScript Playground\***[1] 。

并且还可以看看生成对应的 *TS* 转化 *ES5* ，*ES6* 之后的代码。

## *Type*^类型^

*TypeScript* 的数据类型简单可以分为以下几类：

1. 基本类型

*string*, *number*, *boolean*, *symbol*, *bigint*, *null*, *undefined*

1. 引用类型

*array*,  *Tuple*元组,  *object*包含*Object*和*{}*, *function*

1. 特殊类型

*any*, *unknow*, *void*, *nerver*, *enum*

1. 别名与接口

*type*, *interface*

1. 其他类型

*类型推理*, *字面量类型*, *交叉类型*

TypeSc*r*ipt 只会在编译阶段对类型进行静态检查，如果发现有错误，编译时就会报错。而在运行时，编译生成的 *JS* 与普通的 *JavaScript* 文件一样，并不会进行类型检查。

### *Basic*^基本类型^

```
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

:memo: *Note*

1. *null* 和 *undefined* 两个类型一旦赋值上，就不能在赋值给任何其他类型
2. *symbol* 是独一无二的，假设再定义一个 `sym1` ，那么

```
let sym = Symbol();
let sym1 = Symbol();

sym === sym1; //false
```

### *Reference*^引用类型^

#### *Array*^数组^

两种使用方式：

1. T + `[]`
2. `Array<T>`：泛型*^genertic^* 语法

```
let arr1: number[] = [1, 2, 3]

let arr2: Array<number> = [1, 2, 3]

let arr3: Array<number> = [1, 2, '3'] // error
// TS2322: Type 'string' is not assignable to type 'number'.

// 支持多种类型，使用｜符号
let arr4: Array<number | string> = [1, 2, '3'] //ok
```

#### *Tuple*^元组^

*Tuple* 可以说是 *Array* 的一种特殊情况。

`arr3` 的类型可以是 *string* 也可以是 *number* ，但对每个元素没有作出具体的限制。

那么 *Tuple* 的作用就是限制 **元素的类型** 并且 **限制个数** 的数组，同时 `Tuple`这个概念只存在于 *TS* ，在 *JS* 上是不存在的。

这里存在一个问题：在 *TS* 中，是允许对 *Tuple* 扩增的（也就是允许使用 *push* 方法），但在 **访问上不允许** 。

```
let t: [number, string] = [1, '2']; // ok

let t1: [number, string] = [1, 3]; // error
// TS2322: Type 'number' is not assignable to type 'string'.

let t2: [number, string] = [1]; // error
// TS2322: Type '[number]' is not assignable to type '[number, string]'.  Source has 1 element(s) but target requires 2.

let t3: [number, string] = [1, '1', true]; // error
// Source has 3 element(s) but target allows only 2.

let t5: [number, string] = [1, '2']; // ok
t.push(2); // 允许通过push对tuple扩增，但并不能被访问
console.log(t) // [1, '2', 2]

let a =  t[0]; // ok
let b = t[1]; // ok

let c = t[2]; // error
// TS2493: Tuple type '[number, string]' of length '2' has no element at index '2'.
```

*TypeScript 4.0* 开始，支持为元组类型设置标签：

```
function addPerson(...args: [name: string, age: number]): void {
  console.log(`Person info: name: ${args[0]}, age: ${args[1]}`);
}
```

之后，当我们使用 `addPerson` 方法时，*TypeScript* 的智能提示就会变得更加友好。

```
// 未使用标签的智能提示
// addPerson(args_0: string, args_1: number): void
function addPerson(...args: [string, number]): void {
  console.log(`Person info: name: ${args[0]}, age: ${args[1]}`)
}

// 设置类型标签后的智能提示
// addPerson(name: string, age: number): void
function addPerson2(...args: [name: string, age: number]): void {
  console.log(`Person info: name: ${args[0]}, age: ${args[1]}`);
} 
```

#### *Object*^对象^

##### *object*首字母小写

*object* 表示非原始类型。在定义上直接使用 *object* 是可以的，但不能更改对象的属性，原因是并没有使对象的内部具体的属性做限制，所以需要使用 `{}` 来定义内部类型

```
let obj1: object = {a: 1, b: 2}
obj1.a = 3 // error
// Property 'a' does not exist on type 'object'.(2339)

let obj2: { a: number, b: number } = {a: 1, b: 2}
obj2.a = 3 // ok
```

##### *Object*^首字母大写^

*Object* 表示 *Object* 类的实例，也即除了 *null* 和 *undefined* 的所有类型。（这是因为， *Function* 类型也是由 *Object* 继承而来 ）

```
let obj: Object;
obj = null; // error
// Type 'null' is not assignable to type 'Object'.(2322)
obj = undefined; // error
// Type 'undefined' is not assignable to type 'Object'.(2322)

obj = 1; // ok
obj = "a"; // ok
obj = true; // ok
obj = {}; // ok
obj = Symbol() //ok
// BigInt literals are not available when targeting lower than ES2020.
obj = 10n //ok
```

:memo: *Note*

1. *Object* 接口定义了 *Object.prototype* 原型对象上的属性

```
// node_modules/typescript/lib/lib.es5.d.ts
interface Object {
  constructor: Function;
  toString(): string;
  toLocaleString(): string;
  valueOf(): Object;
  hasOwnProperty(v: PropertyKey): boolean;
  isPrototypeOf(v: Object): boolean;
  propertyIsEnumerable(v: PropertyKey): boolean;
}
```

1. *ObjectConstructor* 接口定义了 *Object* 类的属性

```
// node_modules/typescript/lib/lib.es5.d.ts
interface ObjectConstructor {
  /** Invocation via `new` */
  new(value?: any): Object;
  /** Invocation via function calls */
  (value?: any): any;
  readonly prototype: Object;
  getPrototypeOf(o: any): any;
  // ···
}

declare var Object: ObjectConstructor;
```

*Object* 类的所有实例都继承了 *Object* 接口中的所有属性。

##### *{}*^空对象^

类型描述了一个没有成员的对象。当你试图访问这样一个对象的任意属性时，*TypeScript* 会产生一个编译时错误。

```
// Type {}
const obj = {};

// Error: Property 'prop' does not exist on type '{}'.
obj.prop = "semlinker";
```

但是，你仍然可以使用在 *Object* 类型上定义的所有属性和方法，这些属性和方法可通过 *JavaScript* 的原型链隐式地使用：

```
// Type {}
const obj = {};

// "[object Object]"
obj.toString();
```

#### *Function*^函数^

```
classDiagram
  direction LR
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

##### 定义函数

有两种定义方式：一种为 *function*， 另一种为 **箭头函数** 。

在书写的时候，也可以写入返回值的类型，如果写入，则 **必须** 要有对应类型的返回值，但通常情况下可以 **省略** ，因为 *TS* 的类型推断功能够正确推断出返回值类型。

```
function setName1(name: string) { //ok
  console.log("hello", name);
}

setName1("Domes"); // "hello",  "Domes"

function setName2(name: string): string { //error
  // TS2355: A function whose declared type is neither 'void' nor 'any' must return a value.
  console.log("hello", name);
}

setName2("Domes");

function setName3(name: string): string { //error
  console.log("hello", name);
  return 1;
  // TS2322: Type 'number' is not assignable to type 'string'.
}

setName3("Domes");

function setName4(name: string): string { //ok
  console.log("hello", name);
  return name;
}

setName4("Domes"); // "hello",  "Domes"

// 箭头函数与上同理，不过写在内部
const setName5 = (name: string) => console.log("hello", name);
setName5("Domes") // "hello",  "Domes"
```

##### 参数类型

1. 可选参数： 如果函数要配置可有可无的参数时，可以在形参数后加上 `?` 实现，注意可选参数要放在最后面

```
TS1016: A required parameter cannot follow an optional parameter.
```

1. 默认参数：函数内可以自己设定其默认参数，用 `=` 实现
2. 剩余参数：仍可以使用扩展运算符 `...`

```
/* 1. 可选参数 */
const setInfo1 = (name: string, age?: number) =>
    console.log(name, age)
setInfo1('Domesy') //"Domesy",  undefined
setInfo1('Domesy', 7) //"Domesy",  7

/* 2. 默认参数 */
const setInfo2 = (name: string, age: number = 11) =>
    console.log(name, age)
setInfo2('Domesy') //"Domesy",  11
setInfo2('Domesy', 7) //"Domesy",  7

/* 3. 剩余参数 */
const allCount = (...numbers: number[]) =>
    console.log(`数字总和为：${numbers.reduce((val, item) =>
        (val += item), 0)}`);
allCount(1, 2, 3); //"数字总和为：6"
```

##### 函数重载

是使用 **相同名称** 和 **不同参数数量或类型** 创建多个方法的一种能力。

*TypeScript* 允许在同一范围中声明几个功能类似的 **同名** 函数，表现为给同一个函数提供多个函数类型定义，常用来实现功能类似而所处理的数据类型不同的问题。

:memo: *Note**TS* 引擎按照自上而下的顺序查找重载表，因此要把最精确的定义放在最前面，以减少查找时间。

```
let obj: any = {};

// 重载列表
function setInfo(val: string): void;
function setInfo(val: number): void;
function setInfo(val: boolean, val2): void;
// 实际函数
function setInfo(val: string | number | boolean, val2?): void {
  if (typeof val === "string") {
    obj.name = val;
  } else {
    obj.age = val;
  }
  val2 = val;
}

setInfo("Domes");
setInfo(7);
setInfo(true, 'any');
console.log(obj); // { name: 'Domes', age: 7 }
```

##### *ReturnType*

获取函数返回值

```
type Bar = string;
type foo = () => Bar;
type baz = ReturnType<foo>;
```

### *Wildcard*^通配类型^

#### *Any*

在 *TS* 中，任何类型都可以归于 *any* 类型，所以 *any* 类型也就成了所有类型的顶级类型，同时，如果不指定变量的类型，则默认为 *any* 类型，当然不推荐使用该类型，因为这样丧失了 *TS* 的作用，而且写和不写没什么区别。

```
let d:any; //等价于 let d
d = '1';
d = 2;
d = etrue;
d = [1, 2, 3];
d = {}
```

:memo: *Note*类型推论

如果不设置类型，并且不进行赋值时，将会被被自动推论为 *any* 类型，如果对其进行赋值就会默认为该类型。

```
let any; // 推断为any
let str = 'foo'; // 推断为string
let num = 1; // 推断为number
let flag = false; // 推断为boolean

str = true;
// TS2322: Type 'boolean' is not assignable to type 'string'.
num = 'bar';
// TS2322: Type 'string' is not assignable to type 'number'.
flag = 0;
// TS2322: Type 'number' is not assignable to type 'boolean'.
```

#### *Unknow*

*unknow* 与 *any* 一样，都可以作为所有类型的 **顶级类型** ，但 *unknow* 更加**严格**，只能被赋值给 *any* 类型和 *unknown* 类型本身。不允许定义的值有任何操作（如 方法，*new*等），但 *any* 可以。

```
let u:unknown;
let a: any;

u = '1'; //ok
u = 2; //ok
u = true; //ok
u = [1, 2, 3]; //ok
u = {}; //ok

let value:any = u //ok
let value1:any = a //ok
let value2:unknown = u //ok
let value3:unknown = a //ok
let value4:string = u //error
let value5:string = a //ok
let value6:number = u //error
let value7:number = a //ok
let value8:boolean = u //error
let value9:boolean = a //ok

u.set() // error
a.set() //ok
u() // error
a() //ok
new u() // error
new a() //ok
```

#### *Void*

*void* 当一个函数，没有返回值时，*TS* 会默认它的返回值为 *void* 类型，实际为 *undefined* 。

```
const setInfo = ():void => {}
// 等价于 const setInfo = () => {}

const setInfo1 = ():void => { return '1' }  // error
const setInfo2 = ():void => { return 2 } // error
const setInfo3 = ():void => { return true } // error
const setInfo4 = ():void => { return  } // ok
const setInfo5 = ():void => { return undefined } //ok
```

#### *Never*

*never* 表示一个函数永远不存在返回值，*TS* 会认为类型为 *never* ，那么与 *void* 相比， *never* 应该是 *void* 子集， 因为 *void* 实际上的返回值为 *undefined* ，而 *never* 连 *undefined* 也不行

符合 *never* 的情况有：当抛出异常的情况和无限死循环

```
let error = (): never => {
  // 等价于 let error = () => {}
  throw new Error("error");
};

let _while = (): never => {
  while(true){}
}
```

💡 *Trick*^⭐️^ 全面性检查

在 *TypeScript* 中，可以利用 *never* 类型的特性来实现全面性检查，具体示例如下：

:page_with_curl: *Example*

```
type Foo = string | number;

function controlFlowAnalysisWithNever(foo: Foo) {
  if (typeof foo === "string") {
    // 这里 foo 被收窄为 string 类型
  } else if (typeof foo === "number") {
    // 这里 foo 被收窄为 number 类型
  } else {
    // foo 在这里是 never
    const check: never = foo;
  }
}
```

注意在 *else* 分支里面，我们把收窄为 *never* 的 *foo* 赋值给一个显示声明的 *never* 变量。如果一切逻辑正确，那么这里应该能够编译通过。但是假如后来有一天你的同事修改了 *Foo* 的类型：

```
type Foo = string | number | boolean;
```

然而他忘记同时修改 `controlFlowAnalysisWithNever` 方法中的控制流程，这时候 *else* 分支的 *foo* 类型会被收窄为 *boolean* 类型，导致无法赋值给 *never* 类型的 `check` 变量，这时就会产生一个编译错误。通过这个方式，我们可以确保 `controlFlowAnalysisWithNever` 方法总是穷尽了 *Foo* 的所有可能类型。

通过这个示例，我们可以得出一个结论：使用 *never* 避免出现新增了联合类型没有对应的实现，目的就是写出类型绝对安全的代码。

### *Enum*^枚举^

枚举类型，可以定义一些带名字的常量。

:memo: *Note*

1. 枚举的类型只能是 *string* 或 *number*
2. 定义的名称不能为 **关键字**

#### 数字枚举

枚组的类型默认为 **数字类型** ，默认从 *0* 开始以此累加，如果有设置默认值，则会对 **后面** 的值产生影响

同时支持类似数组下标方式访问的 **反向映射** 。

```
// TypeScript
enum numberType {
  A,
  B,
  C = 7,
  D
}

let num1 = numberType.A // 正向映射
let num2 = numberType[0] // 反向映射
let num3 = numberType[2]
let num4 = numberType[3]

console.log(
    num1,
    num2,
    num3,
    num4
);
```

编译为 *JavaScript* 效果：

```
// ==> ES2020
var numberType;
// 编译后为var，使得该枚举成为了一个全局变量
(function (numberType) {
  numberType[numberType["A"] = 0] = "A";
  numberType[numberType["B"] = 1] = "B";
  numberType[numberType["C"] = 7] = "C";
  numberType[numberType["D"] = 8] = "D";
})(numberType || (numberType = {}));
let num1 = numberType.A; // 正向映射
let num2 = numberType[0]; // 反向映射
let num3 = numberType[2];
let num4 = numberType[3];
console.log(num1, num2, num3, num4);
numberType:
{0:'A', 1:'B', 7:'C', 8:'D', A:0, B:1, C:7, D:8}
```

#### 字符串枚举

字符串枚举要注意的是必须要有 **默认值** ，不支持 **反向映射** 。

```
// TypeScript
enum stringType {
  A = 'A',
  B = 'B',
  C = 'C',
  D = 'D',
  // E
  /* TS1061: Enum member must have initializer. */
  /* 使用字符串枚举的时候，后面的枚举成员必须先初始化 */
}
```

编译为 *JavaScript* 效果：

```
// ==> ES2020
var stringType;
(function (stringType) {
  stringType["A"] = "A";
  stringType["B"] = "B";
  stringType["C"] = "C";
  stringType["D"] = "D";
  // E
  /* TS1061: Enum member must have initializer. */
  /* 使用字符串枚举的时候，必须初始化 */
})(stringType || (stringType = {}));
```

#### 异构枚举

包含了 数字类型*:array* 和 字符串类型*:string* 的混合，同样字符串枚举类型也不支持反向映射。

```
// TypeScript
enum mixedType {
  A,
  B,
  C = "C",
  D = "D",
  E = 7,
  F
}
```

编译为 *JavaScript* 效果：

```
// ==> ES2020
var mixedType;
(function (mixedType) {
  mixedType[mixedType["A"] = 0] = "A";
  mixedType[mixedType["B"] = 1] = "B";
  mixedType["C"] = "C";
  mixedType["D"] = "D";
  mixedType[mixedType["E"] = 7] = "E";
  mixedType[mixedType["F"] = 8] = "F";
})(mixedType || (mixedType = {}));
```

#### 常量枚举

除了 数字类型*:array* 和 字符串类型*:string* 之外，还有一种特殊的类型，那就是 **常量枚举**，也就是通过 *const* 去定义 *enum* ，但这种类型不会编译成任何 *JS* ，而是直接编译对应的值。

:memo: *Note*并且，添加了 *const* 关键字后，后面必须使用相应实例，否则 *TypeScript* 将不会进行编译。

也就是说，普通情况下将会创建一个闭包，并将生成的数组传入 *var* 前缀的全局变量；而变为常量枚举后，则是直接将枚举值硬编码进相应函数中。

```
// TypeScript
const enum constType {
  A,
  B,
  C = 7,
  D
}

let con1 = constType.A;
let con2 = constType.C;
```

编译为 *JavaScript* 效果：

```
// ==> ES2020
let con1 = 0 /* A */;
let con2 = 7 /* C */;
```

### *Literal*^字面量类型^

可以直接指定参数的可选 字面量*^literal^* ，多个字面量通过 `|` 分隔 ，目前支持 字符串*string*、数字*number*、布尔*boolean* 类型。

```
let str:'foo'|'bar'
// str变量的值只能是foo或bar
let num: 1 | 2 | 3 = 1
let flag:true

str = 'foo' //ok
str = 'bar' // ok
str = 'baz' // error
// TS2322: Type '"baz"' is not assignable to type '"foo" | "bar"'.

num = 2 //ok
num = 7 // error
// TS2322: Type '7' is not assignable to type '1 | 2 | 3'

flag = true // ok
flag = false // error
// TS2322: Type 'false' is not assignable to type 'true'.
```

#### *Template*^模板字面量^

模板字面量类型以 字符串字面量类型*^literal^* 为基础，可以通过 联合类型*^union^* 扩展成多个字符串。

它们跟 *JavaScript* 的模板字符串是相同的语法，但是只能用在类型操作中。当使用模板字面量类型时，它会替换模板中的变量，返回一个新的字符串字面量：

```
type world = "world";
type World = "World";

type Greeting = `hello ${world | World}`;
// type Greeting = "hello world"
```

#### *Intrinsic*^内置字符操作类型^

*TypeScript* 的一些类型可以用于字符操作，这些类型处于性能的考虑被内置在编译器中，不能在 `.d.ts` 文件里找到它们。

模版: `Operation<type>`

1. *Uppercase* - 把每个字符转为大写形式
2. *Lowercase* - 把每个字符转为小写形式
3. *Capitalize* - 把字符串的第一个字符转为大写形式
4. *Uncapitalize* - 把字符串的第一个字符转换为小写形式

### *Aliases*^类型别名^

*type* 用来给一个类型起个别名。

```
type InfoProps = string | number;
const setInfo = (data: InfoProps) => {};
```

## *Assertion*^断言^

### *As*^类型断言^

类型断言*Type Assertion* 可以用来手动指定一个值的类型。用途：

1. 将一个 联合类型*^union^* 断言为其中一个类型语法
2. 将一个 父类*^parent^* 断言为更加具体的 子类*^child^*
3. 将任何一个类型断言为 *any* / 将 *any* 断言为具体类型

```
值 as 类型
<类型>值
```

:page_with_curl: *Example*

```
//尖括号
let num: any = 'foo'
let res1: number = (<string>num).length; // React中会 error

// as 语法
let str: any = 'bar';
let res: number = (str as string).length;
```

:warning: *Caution*尖括号语法在 *React* 中会报错，原因是与 *JSX* 语法会产生冲突，所以只能使用 *as* 。

### *As^..as..^*^双重断言^

使用类似 `as any as Foo` 的语法，对变量进行两次断言，来达到将任何一个类型断言为任何另一个类型的效果。

:warning: *Caution*这种做法相当于抛弃了 *TypeScript* ，非常容易导致运行时错误，不推荐使用。

```
interface Cat {
  run(): never;
  swim(): string
}

interface Fish {
  swim(): string;
}

function cat2Fish(cat: { run(): void; swim(): void }) {
  return (cat as any as Fish);
}

class Fish implements Fish {}

let cat = new class Cat implements Cat {
  run() {}

  swim() {
    return 'cat.swim'
  }
}

console.log(cat2Fish(cat).swim());
// implemented as Fish
// cat.swim
```

### *!^for-key^*^确定赋值断言^

确定赋值断言，即允许在 实例属性*^properties^* 和 变量声明*^statement^* 后面放置一个 `!` 号，以告诉 *TS* 该属性会被明确赋值。

```
let foo: string;
let bar!: string;

const setFoo = () => foo = 'foo'
const setBar = () => bar = 'bar'

setFoo();
setBar();

console.log(foo); // error
// Variable 'foo' is used before being assigned.
console.log(bar); // ok
```

### *!^for-value^*^非空断言^

在上下文中当类型检查器无法断定类型时，一个新的后缀表达式操作符 `!` 可以用于断言操作对象是非 *null* 和非 *undefined* 类型。

```
const info = (str: string | null | undefined) => {
  const name: string = str;
  // Type 'undefined' is not assignable to type 'string'.(2322)

  const name2: string = str!; // 添加!符号进行非空断言
};
info('foo');
```

## *Guards*^类型守卫^

*Type guards* 是可执行运行时检查的一种表达式，用于确保该类型在一定的范围内。使用守卫进行 *Type narrowing* 后，就可以使用相应的类型方法和属性了 。

类型保护可以保证一个字符串是一个字符串，尽管它的值也可以是一个数值。类型保护与特性检测并不是完全不同，其主要思想是尝试检测属性、方法或原型，以确定如何处理值。

### *In*^成员检测^

用于判断某个 属性*^property^* 是否存在于 对象*^object^* 当中。

```
interface Employee {
  name: string
  salary: number
}

interface Manager extends Employee {
  isManager: true
}

const printInfo = (data: Employee | Manager) => {
  console.log(`该 ${"isManager" in data ? `经理` : `雇员`}名字是：${data.name}，薪水是：${data.salary}`)
}

printInfo({name: 'David', salary: 2000});
printInfo({name: 'White', salary: 7000, isManager: true});
// 该雇员名字是：David，薪水是：2000
// 该经理名字是：White，薪水是：7000
```

### *Typeof*^类型检测^

用于 变量*^variable^* 是否属于某个 基本类型*basic-type instance* ，见 *EcmaScript* [*typeof*](04 JavaScript.md/#variable-typeof-es5 "*typeof*") 。

### *Instanceof*^实例检测^

用于判断一个 对象*^object^* 是不是某个 类*^class^* 的 实例*^instance^* ，见 *EcmaScript* [*instanceof*](05 EcmaScript.md/#class-instanceof-usage-es6 "*instanceof*") 。

### *Is*

*is* 关键字用于定义类型保护，用于自定义函数返回类型。

当类型符合的时候，可以直接调用类型相应的方法。

```
class Fish {
  swim() {
    console.log('swimming');
  }
}

class Bird {
  fly() {
  }
}

function getSmallPet() {
  return new Fish();
}

function isFish(pet: Fish | Bird): pet is Fish {
  // 告诉编译器将会返回Fish类型
  return (pet as Fish).swim !== undefined;
}


// Both calls to 'swim' and 'fly' are now okay.
let pet = getSmallPet();

pet.swim();
if (isFish(pet)) {
  pet.swim();
}
```

通过上面的介绍，我们可以发现 *assertion*^断言^ 与 类型守卫 的概念非常相似，都是确定参数的类型，但 *assertion*^断言^ 它是直接告诉编辑器，这个参数就是这个类型，而类型守卫更像判断这个参数具体是什么类型。

## *Combine*^类型组合^

### *Union*^联合类型^*^|^*

使用 `|` 符号连接，将多个类型合并为一个类型*^type/interface^* 并集，使得这个类型可以是多种类型 **之一** 。在使用 **类型守卫\*^guards^\***[2] 进行 *Narrowing* 之前，只能使用类型中共有的方法。

联合类型通常与 *null* 或 *undefined* 一起使用：

```
const sayHello = (name: string | undefined) => {
  /* ... */
};
```

例如，这里 `name` 的类型是 `string|undefined` 意味着可以将 *string* 或 *undefined* 的值传递给 `sayHello` 函数。

```
sayHello("semlinker");
sayHello(undefined);
sayHello(123); // error
```

通过这个示例，你可以凭直觉知道类型 `A` 和类型 `B` 联合后的类型是同时接受 `A` 和 `B` 值的类型。此外，对于联合类型来说，你可能会遇到以下的用法：

```
let num: 1 | 2 = 1;
type EventNames = 'click' | 'scroll' | 'mousemove';
let event:EventNames = 'foo'; // error
```

以上示例中的 `1`、`2` 或 `'click'` 被称为字面量类型，用来约束取值只能是某几个值中的一个。

#### *Discriminated Unions*^可辨识联合^

可辨识联合类型是 *TypeScript* 一个模仿 *Haskell* 的概念，也称为代数数据类型或标签联合类型。

这种类型的本质是结合 联合类型*^union^* 和 字面量类型 的一种类型保护方法。如果一个类型是多个类型的联合类型，且多个类型含有一个 **公共属性** ，那么就可以利用这个公共属性，来创建相似的类型 接口*^interface^* 组。

##### *Discriminantable*^可辨识^

可辨识要求联合类型中的每个元素都至少含有一个 **相同** 单例类型属性，比如：

```
const enum CarTransmission {
  Automatic = 200,
  Manual = 300
}

interface Motorcycle {
  vType: "motorcycle"; // discriminant
  make: number; // year
}

interface Car {
  vType: "car"; // discriminant
  transmission: CarTransmission
}

interface Truck {
  vType: "truck"; // discriminant
  capacity: number; // in tons
}
```

在上述代码中，我们分别定义了 `Motorcycle`、 `Car` 和 `Truck` 三个接口，在这些接口中都包含一个 `vType` 属性，该属性被称为可辨识的属性，而其它的属性只跟特性的接口相关。

:page_with_curl: *Example**Narrowing*

经过 *Type Guards* 的 *Narrowing* 后，就可以使用相应的方法了。

```
type Shape =
  | { kind: "circle"; radius: number }
  | { kind: "square"; x: number }
  | { kind: "triangle"; x: number; y: number };

function area(s: Shape) {
  switch (s.kind) {
    case "circle": // Type Narrowing
      return Math.PI * s.radius * s.radius;
    case "square":
      return s.x * s.x;
    case "triangle":
      return (s.x * s.y) / 2;
  }
  // 当类型无法收窄至上述类型，就会报错
  const check: never = s;
}
```

编译成 *JavaScript* ：

```
"use strict";
function area(s) {
  switch (s.kind) {
    case "circle":
      return Math.PI * s.radius * s.radius;
    case "square":
      return s.x * s.x;
    case "triangle":
      return (s.x * s.y) / 2;
  }
  const check = s;
}
```

##### *Combine*^联合类型^

基于前面定义了三个接口，我们可以创建一个 `Vehicle` 联合类型：

```
type Vehicle = Motorcycle | Car | Truck;
```

现在我们就可以开始使用 `Vehicle` 联合类型，对于 `Vehicle` 类型的变量，它可以表示不同类型的车辆。

##### *Guard*^类型守卫^

下面我们来定义一个 `evaluatePrice` 方法，该方法用于根据车辆的类型、容量和评估因子来计算价格，具体实现如下：

```
const EVALUATION_FACTOR = Math.PI; 

function evaluatePrice(vehicle: Vehicle) {
  return vehicle.capacity * EVALUATION_FACTOR; // err
  // Property 'capacity' does not exist on type 'Vehicle'.
  // Property 'capacity' does not exist on type 'Motorcycle'.(2339)
}

const myTruck: Truck = { vType: "truck", capacity: 9.5 };
evaluatePrice(myTruck);
```

该代码将会报错，原因是在 *Motorcycle* 接口中，并不存在 `capacity` 属性，而对于 `Car` 接口来说，它也不存在 `capacity` 属性。那么，现在我们应该如何解决以上问题呢？这时，我们可以使用 类型守卫*type guard* 。下面我们来重构一下前面定义的 `evaluatePrice` 方法，重构后的代码如下：

```
function evaluatePrice(vehicle: Vehicle) {
  switch (vehicle.vType) {
    case "car":
      return vehicle.transmission * EVALUATION_FACTOR;
    case "truck":
      return vehicle.capacity * EVALUATION_FACTOR;
    case "motorcycle":
      return vehicle.make * EVALUATION_FACTOR;
  }
}
```

在以上代码中，我们使用 `switch` 和 `case` 运算符来实现类型守卫，从而确保在 `evaluatePrice` 方法中，我们可以安全地访问 `vehicle` 对象中的所包含的属性，来正确的计算该车辆类型所对应的价格。

##### *Alias*^类型别名^

类型别名用来给一个类型起个新名字。

```
type Message = string | string[];

let greet = (message: Message) => {
  // ...
};
```

### *Intersect*^交叉类型^*^&^*

使用 `&` 符号连接，将 **多个类型** 合并为 **一个** 拥有它们 属性*^property^* 并集 的类型。

```
type AProps = { foo: string }
type BProps = { bar: number }

type allProps = AProps & BProps

const Info: allProps = {
  foo: '1',
  bar: 2
}
```

#### *Basic*^同名基础属性合并^

我们可以看到 `交叉类型` 是结合两个属性的属性值，那么我们现在有个问题，要是两个属性都有相同的属性值，那么此时总的类型会怎么样，先看看下面的案列：

```
type AProps = { a: string, c: number }
type BProps = { b: number, c: string }

type allProps = AProps & BProps

const Info: allProps = {
  a: '1',
  b: 2,
  c: 3, // TS2322: Type 'number' is not assignable to type 'never'.
  c: '4', // TS2300: Duplicate identifier 'c'.
  // TS2322: Type 'string' is not assignable to type 'never'.
  // ts.ts(1, 28): The expected type comes from property 'c' which is declared here on type 'allProps'
}
```

如果是相同的类型，合并后的类型也是此类型，那如果是不同的类型会如何：

我们在 `Aprops` 和 `BProps` 中同时加入 `c` 属性，并且 `c` 属性的类型不同，一个是 *number* 类型，另一个是 *string* 类型。

现在结合为 `allProps` 后呢? 是不是 `c` 属性是 *number* 或 *string* 类型都可以，还是其中的一种？

然而在实际中， `c` 传入 数字类型*number* 和 字符串类型*string* 都不行，因此看到报错，现实的是 `c` 的类型是 *never* 。

这是因为对应 `c` 属性而言是 *number & string* ，然而这种属性明显是不存在的，所以 `c` 的属性是 *never* ，即不能为任何值。

#### *Reference*^同名非基础属性合并^

```
interface A { a: number }
interface B { b: string }

interface C {
  x: A
}
interface D {
  x: B
}
type allProps = C & D

const Info: allProps = {
  x: {
    a: 0,
    b: '1'
  }
}

console.log(Info); // { x: { a: 0, b: '1' } }
```

我们来看看案例，对于混入多个类型时，若存在相同的成员，且成员类型为非基本数据类型，那么是可以成功合合并。

如果 接口 `A` 中的也是 `b` ，类型为 *number* ，就会跟 **同名基础属性合并** 一样，变为 *never* 类型。

## *Interfaces*^接口^

在 *TypeScript* 中，使用 接口*^Interfaces^* 来定义对象的类型。

在面向对象语言中，接口*^Interfaces^* 是一个很重要的概念，它是对行为的抽象，而具体如何行动需要由 类*^classes^*去 实现*^implement^* 。

*TypeScript* 中的接口是一个非常灵活的概念，除了可用于对类的一部分行为进行 抽象*^abstract^* 以外，也常用于对对象的 形状*^Shape^* 进行描述。

### *Shape*^对象的形状^

```
interface Shape {
    height: bigint,
    width: bigint
}

let rectangle: Shape = {
    height: 10n,
    width: 10n
};
```

上面的例子中，我们定义了一个接口 `Shape` ，接着定义了一个变量 `rectangle`，它的类型是 `Shape`。这样，我们就约束了 `rectangle` 的形状必须和接口 `Shape` 一致。

接口一般首字母大写，内部变量的形状必须和接口的形状保持一致。

### *?*^可选属性^

有时我们希望不要完全匹配一个形状，那么可以用可选属性，该属性可以不存在，且位置任意。

```
interface Shape {
    height: bigint,
    note?: string,
    width: bigint
}

let rectangle: Shape = {
    height: 10n,
    width: 10n
};
```

### *Any*^任意属性^

有时候我们希望一个接口成员允许有任意的属性类型，可以使用如下方式：

```
interface Person {
  name: string;
  note: any;
}
```

使用 `[propName: string]` 定义了任意属性取 `string` 类型的值。

### *Readonly*^只读属性^

有时候我们希望对象中的一些 **字段** 只能在 **创建的时候被赋值** ，那么可以用 *readonly* 定义只读属性。

定义后，只允许一次初始化，之后便不允许修改。

🧪 *Experimental**const* 可能只能影响变量，而不能影响成员。

```
interface Person {
    readonly id: number;
    name: string;
    age?: number;
    [propName: string]: any;
}

let tom: Person = {
    id: 89757,
    name: 'Tom',
    gender: 'male'
};

tom.id = 9527;

// index.ts(14,5): error TS2540: Cannot assign to 'id' because it is a constant or a read-only property.
```

上例中，使用 *readonly* 定义的属性 `id` 初始化后，又被赋值了，所以报错了。

:exclamation:*Warning*只读*^readonly^* 的约束存在于第一次给 对象*^object^* 赋值的时候，而不是第一次给只读属性赋值的时候。

:memo: *Note 1*可以理解为，初始化对象的时候，就必须提供一个初始值。

```
interface Person {
    readonly id: number;
    name: string;
    age?: number;
    [propName: string]: any;
}

let tom: Person = {
    name: 'Tom',
    gender: 'male'
};

tom.id = 89757;

// Attempt to assign to const or readonly variable 
// TS2540: Cannot assign to 'id' because it is a read-only property
```

上例中，报错信息有两处，第一处是在对 `tom` 进行赋值的时候，没有给 `id` 赋值。

第二处是在给 `tom.id` 赋值的时候，由于它是只读属性，所以报错了。

:memo: *Note 2*此外 *TypeScript* 还提供了 `ReadonlyArray<T>` 数组范型*^genertic^* ，它与 `Array<T>` 相似，只是把所有可变方法去掉了，因此可以确保数组创建后再也不能被修改。

### *Signatures*^索引签名^

有时并不提前知道类型属性的所有名称，但知道值的 形状*^shape^* 。此时可以使用 索引签名*index signatures* （类似方括号语法）来描述可能值的类型。值*^key^* 的可选类型有 *string, number, symbol* 。

```
interface NumberOrStringDictionary {
  [index: string]: number | string;
  length: number; // ok, length is a number
  name: string; // ok, name is a string
}
```

当 值*^value^* 类型不符时，就会报错：

```
interface NumberDictionary {
  [index: string]: number;

  length: number; // ok
  name: string; // error
}
```

### *Mapped*^映射类型^

映射类型建立在 索引签名*index signatures* 的语法之上，用于声明未提前声明的属性类型：

```
type OnlyBoolsAndHorses = {
  [key: string]: boolean | Horse;
};
 
const conforms: OnlyBoolsAndHorses = {
  del: true,
  rodney: false,
};
```

当 键名*^key^* 类型不符时，就会报错：

```
interface NumberDictionary {
  [index: string]: number;
 
  length: number; // ok
  name: string; // error
}
```

### ^⭐️^*Distinguish*^辨别^

:star: *Important**Alias*^类型别名^ 和 *interface*^接口^ 的区别

#### *Objects*

#### *Functions*

接口和类型别名都可以用来描述对象的形状或函数签名：

##### *Interface*^接口^

```
interface Point {
  x: number;
  y: number;
}

interface SetPoint {
  (x: number, y: number): void;
}
```

##### *Alias*^类型别名^

```
type Point = {
  x: number;
  y: number;
};

type SetPoint = (x: number, y: number) => void;
```

#### *Other Types*

与接口类型不一样，类型别名可以用于一些其他类型，比如原始类型、联合类型和元组：

```
// primitive
type Name = string;

// object
type PartialPointX = { x: number; };
type PartialPointY = { y: number; };

// union
type PartialPoint = PartialPointX | PartialPointY;

// tuple
type Data = [number, string];
```

#### *Extend*

接口和类型别名都能够被扩展，但语法有所不同。此外，接口和类型别名不是互斥的。接口*^interface^* 可以扩展 类型别名*^alias^* ，而反过来是不行的。

**Interface extends interface**

```
interface PartialPointX { x: number; }
interface Point extends PartialPointX { 
  y: number; 
}
```

**Type alias extends type alias**

```
type PartialPointX = { x: number; };
type Point = PartialPointX & { y: number; };
```

**Interface extends type alias**

```
type PartialPointX = { x: number; };
interface Point extends PartialPointX { y: number; }
```

**Type alias extends interface**

```
interface PartialPointX { x: number; }
type Point = PartialPointX & { y: number; };
```

#### *Implements*

类可以以相同的方式实现 接口*^interface^* 或 类型别名*^type^* ，但类不能实现由 类型别名*^type^* 定义的 联合类型*^union^* ：

```
interface Point {
  x: number;
  y: number;
}

class SomePoint implements Point {
  x = 1;
  y = 2;
}

type Point2 = {
  x: number;
  y: number;
};

class SomePoint2 implements Point2 {
  x = 1;
  y = 2;
}

type PartialPoint = { x: number; } | { y: number; };

// A class can only implement an object type or 
// intersection of object types with statically known members.
class SomePartialPoint implements PartialPoint { // Error
  x = 1;
  y = 2;
}
```

#### *Declaration merging*

与类型别名不同，接口可以定义多次，会被自动合并为单个接口。

```
interface Point { x: number; }
interface Point { y: number; }

const point: Point = { x: 1, y: 2 };
```

## *Class*^类^

*ES6* 中新增了 *class* 关键字，用于定义类。

### *Basic*^基本方法^

包括：静态属性，静态方法、成员属性、成员方法、私有属性、私有方法、构造器、*getter & setter* 。

:memo: *Note*需要注意的是： 在静态方法中，如果不给默认值，并且不使用是会报错的，如果不想报错就使用 `!` 关键字，如：`memberProperty!:string` 。

```
class Class {
    /* 1. 静态属性 */
    static staticProperty: string = '静态属性';
    // static name!:string;
    // TS1255: A definite assignment assertion '!' is not permitted in this context.

    /* 2. 静态方法 */
    static staticMember = () => {
        return `我是静态方法:${this.staticProperty}`;
    }

    /* 3. 成员属性 */
    // 实际上是通过public上进行修饰，只是省略了
    member1: string = '成员属性';
    member2: string; // note: 并没有报错
    memberProperty!: string; // ok 不设置默认值的时候必须加入！

    /* 4. 成员方法 */
    memberMethod = () => {
        return `我是成员方法:${this.memberProperty}`;
    }
    getPrivateMethod = () => {
        return this.#privateMethod();
    }

    /* 5. 私有属性 */
    #privateProperty: string = '私有属性';

    /* 6. 私有方法 */
    #privateMethod = () => {
        return `我是私有方法:${this.#privateProperty}`;
    };

    /* 7. 构造器 */
    constructor(_name: string) {
        this.memberProperty = _name;
    }

    /* 8. get */
    get getter() {
        return this.memberProperty;
    }

    /* ... & set */
    set getter(val) {
        this.memberProperty = val;
    }
}

const instance = new Class('成员属性');
console.log(Class.staticMember());
console.log(instance.getPrivateMethod());
console.log(instance.memberMethod());
// 我是静态方法:静态属性
// 我是私有方法:私有属性
// 我是成员方法:成员属性
```

### *Modifier*^修饰符^

#### *public*^公开^

修饰的属性或方法是公有的，可以在任何地方被访问到，默认所有的属性和方法都是 *public* 的。

#### *protected*^保护^

修饰的属性或方法是受保护的，它和 *private* 类似，但允许被子类继承从而被访问。

#### *private*^私有^

修饰的属性或方法是私有的，不能在声明它的类的外部访问。

:memo: *Note*该限制仅存在于编译期间，编译之后的代码中，并没有限制  *private* 属性在外部的可访问性。

#### *#*^私有字段^

在 *TS 3.8* 版本便开始支持 *ES2022* 新增的私有方法，而翻译成之前的版本则使用 ***WeakMap()\***[3] 实现。

需要注意的是 **私有字段** 与常规字段不同，主要的区别是：

1. 私有字段以 `#` 字符开头，也叫私有名称
2. 每个私有字段名称都 **唯一** 地限定于其包含的类
3. 不能在私有字段上使用 *TypeScript* 可访问性修饰符（如 *public* 或 *private*）
4. 私有字段不能在包含的类之外访问，甚至不能被检测到。

#### *readonly*^只读属性^

见 **接口\*^interface^\***[4] 的只读属性。

:page_with_curl: *Example*

```
class PropertyTest {
    public publicProperty = 'foo';
    private privateProperty = 'bar';
    #property = 'baz';

    method() {
        console.log(this.publicProperty); // foo
        console.log(this.privateProperty); // bar
        // 编译之后的代码中，并没有限制 private 属性在外部的可访问性
         console.log(this.#property); // baz
        // ES2022前，使用WeakMap()保存为真正的私有属性
    }
}

new PropertyTest().method();
```

编译为 *EcmaScript2020* ：

```
// ES2020
"use strict";
var __classPrivateFieldGet = (this && this.__classPrivateFieldGet) || function (receiver, state, kind, f) {
    if (kind === "a" && !f) throw new TypeError("Private accessor was defined without a getter");
    if (typeof state === "function" ? receiver !== state || !f : !state.has(receiver)) throw new TypeError("Cannot read private member from an object whose class did not declare it");
    return kind === "m" ? f : kind === "a" ? f.call(receiver) : f ? f.value : state.get(receiver);
};
var _PropertyTest_property;
class PropertyTest {
    constructor() {
        this.publicProperty = 'foo';
        this.privateProperty = 'bar';
        _PropertyTest_property.set(this, 'baz');
    }
    method() {
        console.log(this.publicProperty); // foo
        console.log(this.privateProperty); // bar
        // 编译之后的代码中，并没有限制 private 属性在外部的可访问性
        console.log(__classPrivateFieldGet(this, _PropertyTest_property, "f")); // baz
        // ES2022前，使用WeakMap()保存为真正的私有属性
    }
}
_PropertyTest_property = new WeakMap();
new PropertyTest().method();
```

### *Extends*^继承^

继承*^Inheritance^* 是一种联结类与类的层次模型。指的是一个类（称为子类、子接口）继承另外的一个类（称为父类、父接口）的功能，并可以增加它自己的新功能的能力，继承是类与类或者接口与接口之间最常见的关系。

见 *EcmaScript* *Class* 一章中的 [继承](05 EcmaScript.md#class-extends-es6 "继承") 。继承是一种 *is-a* 关系：

```
classDiagram
  direction BT
  Class_B --> Class_A
  Interface_B --> Interface_A
  
  class Class_A{
  }
     
  class Class_B{
  }
  
  class Interface_A{
  
  }
  
  class Interface_B{
  
  }
```

### *Implements*^实现^

用于检测某个类是否实现了相应接口，不符合则报错。

```
// @errors: 2420
interface Pingable {
  ping(): void;
}

class Sonar implements Pingable {
  ping() {
    console.log("ping!");
  }
}

class Ball implements Pingable {
  // error, Ball中没有ping()方法
  pong() {
    console.log("pong!");
  }
}
```

### *Abstract*^抽象类^

用 *abstract* 关键字声明的类叫做 **抽象类**，声明的方法叫做 **抽象方法** 。

1. **抽象类**：指不能被实例化，因为它里面包含一个或多个抽象方法。
2. **抽象方法**：是指不包含具体实现的方法；

:memo: *Note*抽象类指的是不能直接实例化，只能实例化实现了所有抽象方法的子类。

:page_with_curl: *Example*

```
abstract class Shape {
    protected readonly name;

    protected constructor({name = ''}) {
        this.name = name;
    }

    // Abstract class constructor can be made protected
    abstract getArea(): number;
}

class Rectangle extends Shape {
    protected readonly height;
    protected readonly width;

    constructor(name, [height = 0, width = 0]) {
        super({name});
        this.height = height;
        this.width = width;
    }

    getArea() {
        return this.height * this.width;
    }
}

class Square extends Rectangle {
    constructor(name, length: number) {
        super(name, [length, length]);
    }
}

class Triangle extends Shape {
    protected readonly height;
    protected readonly width;

    constructor(name, [height = 0, width = 0]) {
        super({name});
        this.height = height;
        this.width = width;
    }

    getArea() {
        return this.height * this.width / 2;
    }
}

console.log(
    new Triangle('triangle', [12, 10]).getArea(),
    new Rectangle('rectangle', [12, 10]).getArea(),
    new Square('square', 10).getArea(),
);
// 60  120  100
```

### *Override & overload*^重写和重载^

1. [**重写***override*](06 EcmaScript C/#class-extends-es6 "**重写***override*")：使用 *extends* 关键字使子类能重写继承自父类中的方法
2. ***\*重载\**\*overload\***[5]：允许同一个函数拥有多个类型定义

### *Infer*^类型推断^

当 `noImplicitAny` 配置属性被启用之后，*TypeScript* 就可以使用控制流分析来确认类中的属性类型：

```
class Person {
   fullName;  // (property) Person.fullName: string
   firstName; // (property) Person.firstName: string | undefined
   lastName; // (property) Person.lastName: string | undefined

   constructor(fullName: string) {
     this.fullName = fullName;
     if(Math.random()){
       this.firstName = fullName.split(" ")[0];
       this.lastName =   fullName.split(" ")[1];
     }
   }  
}
```

:memo: *Note*但在使用过程中，如果我们没法保证对成员属性都进行赋值，那么该属性可能会被认为是 `undefined`。

默认 *TS* 并不会自动推断 类*^class^* 的 成员*^property^* 类型：

```
TS7045: Member 'fullName' implicitly has an 'any' type, but a better type may be inferred from usage.
```

## *Generics*^泛型^

类似 *C++* 和 *Java* 的语法，*TypeScript* 可以在定义函数、接口或类的时候，不预先指定具体的类型，而在使用的时候再指定类型。

```
function identity<T>(value: T): T {
  // T:传递类型 --> T链式传递给参数类型和返回类型
  return value;
}

identity<Number>(1);
```

参考上面的图片，当我们调用 `identity<Number>(1)` ，`Number` 类型就像参数 `1` 一样，它将在出现 `T` 的任何位置填充该类型。

`<T>` 内部的 `T` 被称为 类型变量*type variable* ，在定义泛型时通常用作第一个类型变量名称。但实际上 `T` 可以用任何有效名称代替。它是我们希望传递给 *identity* 函数的类型占位符，同时它被分配给 `value` 参数用来代替它的类型：此时 `T` 充当的是类型，而不是特定的 *Number* 类型。

除了 `T` 之外，以下是常见泛型变量代表的意思：

1. *K* *^key^*：表示对象中的键类型；
2. *V* *^value^*：表示对象中的值类型；
3. *E* *^element^*：表示元素类型。

也就是说，泛型是允许同一个函数接受不同类型参数的一种模版，与 *any* 相比，使用泛型来创建可 复用*^multiplex^* 的组件要更好，因为泛型会保留 参数类型*^type^* 。

其实并不是只能定义一个类型变量，我们可以引入希望定义的任何数量的类型变量。比如我们引入一个新的类型变量 `U` ，用于扩展我们定义的 `identity` 函数：

```
function identity<T, U>(value: T, message: U): T {
  console.log(message);
  return value;
}

console.log(identity<Number, String>(68, 'semi-linker'));
// semi-linker ~> Number --> T  
// 68          ~> String --> U  
```

除了为类型变量显式设定值之外，一种更常见的做法是使编译器自动选择这些类型，从而使代码更简洁。我们可以完全省略尖括号，比如：

```
function identity<T, U>(value: T, message: U): T {
  console.log(message);
  return value;
}

console.log(identity(68, "Semlinker"));
```

对于上述代码，编译器足够聪明，能够知道我们的参数类型，并将它们赋值给 `T` 和 `U` ，而不需要开发人员显式指定它们。

### *Interface*^泛型接口^

```
interface GenericIdentityFn<T> {
  (arg: T): T;
}
```

### *Class*^泛型类^

```
class GenericNumber<T> {
  zeroValue: T;
  add: (x: T, y: T) => T;
}

let myGenericNumber = new GenericNumber<number>();
myGenericNumber.zeroValue = 0;
myGenericNumber.add = function (x, y) {
  return x + y;
};
```

### *Tools*^泛型工具^

#### *Typeof*

在 *TypeScript* 中，*typeof* 操作符可以用来获取一个变量声明或对象的类型。

```
interface Person {
  name: string;
  age: number;
}

const sem: Person = {name: 'semi-linker', age: 33};
type Sem = typeof sem; // -> Person
let Sam: Sem = {name: 'foo', age: 42}

// ok 键名字面量相同、键值类型相同

function toArray(x: number): Array<number> {
  return [x];
}

type Func = typeof toArray; // -> (x: number) => number[]
// Alias for:  typeof toArray
// Initial type:  (x: number) => Array<number>

let func: Func = function (x: number) {
  return [1, 2, 3];
} // ok 参数相同、返回值相同
```

#### *Keyof*

*keyof* 操作符可以用于获取某种类型的所有键，其返回类型是联合类型。

```
interface Person {
  name: string;
  age: number;
}

type K1 = keyof Person; // "name" | "age"

type K2 = keyof Person[];
// 数组类型  Alias for: keyof Person[]/keyof []
// "length" | "toString" | "toLocaleString" | "pop" | "push" | "concat" | "join" | "reverse" | "shift" | "slice" | "sort" | ...

type K3 = keyof { [x: string]: Person };  // string | number
// Alias for:  keyof {[p: string]: Person}
// Initial type:  string | number
```

在 *TypeScript* 中支持两种索引签名，数字索引和字符串索引：

```
interface StringArray {
  // 字符串索引 -> keyof StringArray => string | number
  [index: string]: string;
}

interface NumberArray {
  // 数字索引 -> keyof NumberArray => number
  [index: number]: string;
}
interface Person {
  name: string;
  age: number;
}
```

:memo: *Note*

为了同时支持两种索引类型，就得要求把 数值*^number^* 索引*^index^* 的返回值必须是 字符串*^string^*  索引返回值的 **子类** 。其中的原因就是当使用数值索引时，*JavaScript* 在执行索引操作时，会先把 数值*^number^* 索引先转换为 字符串*^string^* 索引。所以下面 `k` 的类型是 `string|number` 。

:page_with_curl: *Example*

```
interface Person {
  name: string;
  age: number;
}
type k = keyof { [x: string]: Person };
// Alias for: keyof {[p: string]: Person}
// Initial type: string | number
```

#### *In*

`in` 用来遍历 可枚举类型*^iterable-type^* ：

```
type Keys = "a" | "b" | "c"

type Obj = {
  [p in Keys]: any;
} // 遍历Key类型中的所有成员作为键名
// Initial type:  {a: any, b: any, c: any}

type Str = {
  [P in keyof '']: ''[P];
} // 获取字符串中的所有键名: 内容为字符串类型中的所有键值
// Initial type:  {toString(): string, ...
```

#### *Infer*

在条件类型语句中，可以用 `infer` 声明一个类型变量并且对它进行使用。

```
type ReturnType<T> = T extends (
  ...args: any[]
) => infer R ? R : any;
```

以上代码中 `infer R` 就是声明一个变量来承载传入函数签名的返回值类型，简单说就是用它取到函数返回值的类型方便之后使用。

#### *Extends*

有时候我们定义的泛型不想过于灵活或者说想继承某些类等，可以通过 *extends* 关键字添加泛型约束。

```
interface Lengthwise {
  length: number;
}

function loggingIdentity<T extends Lengthwise>(arg: T): T {
  console.log(arg.length);
  return arg;
}
```

现在这个泛型函数被定义了约束，因此它不再是适用于任意类型：

```
loggingIdentity(3); // undefined
```

这时我们需要传入符合约束类型的值，必须包含必须的属性：

```
loggingIdentity({length: 3}); // 3
```

#### *Partial*

`Partial<T>` 的作用就是将某个类型里的属性全部变为可选项 `?` 。

**定义：**

```
/**
 * node_modules/typescript/lib/lib.es5.d.ts
 * Make all properties in T optional
 */
type Partial<T> = {
  [P in keyof T]?: T[P];
};
```

在以上代码中，首先通过 `keyof T` 拿到 `T` 的所有属性名，然后使用 `in` 进行遍历，将值赋给 `P`，最后通过 `T[P]` 取得相应的属性值。中间的 `?` 号，用于将所有属性变为可选。

**示例：**

```
interface Todo {
  title: string;
  description: string;
}

function updateTodo(todo: Todo, fieldsToUpdate: Partial<Todo>) {
  return {...todo, ...fieldsToUpdate};
  // 解构写法
}

const todo1 = {
  title: "Learn TS",
  description: "Learn TypeScript",
};

const todo2 = updateTodo(todo1, {
  description: "Learn TypeScript Enum",
});
```

在上面的 `updateTodo` 方法中，我们利用 `Partial<T>` 工具类型，定义 `fieldsToUpdate` 的类型为 `Partial<Todo>`，即：

```
interface PartiallyTodo {
  title?: string | undefined;
  description?: string | undefined;
}
```

## *Decorator*^装饰器^

随着 *TypeScript* 和 *ES6* 中 类*^class^* 的引入，现在存在某些需要附加功能来支持 注释*^comment^* 或修改类和类成员的场景。装饰器*^decorator^* 提供了一种为类声明和成员添加注释和元编程语法的方法。装饰器是 *JavaScript* 的 *stage2* 提案，可作为 *TypeScript* 的实验性功能使用。它是一个表达式：

1. 该表达式被执行后，返回一个函数
2. 函数的入参分别为 *target*、*name* 和 *descriptor*
3. 执行该函数后，可能返回 *descriptor* 对象，用于配置 *target* 对象

需要注意的是，若要启用实验性的装饰器特性，你必须在命令行或 `tsconfig.json` 里启用 `experimentalDecorators` 编译器选项：

**命令行**：

```
tsc --target ES5 --experimentalDecorators
```

或是在 `tsconfig.json`：

```
{
  "compilerOptions": {
     "target": "ES5",
     "experimentalDecorators": true
   }
}
```

装饰器是一种函数，写成 `@ + 函数名` 。它可以放在类和类方法的定义前面。

```
@frozen class Foo {
  @configurable(false)
  @enumerable(true)
  method() {}

  @throttle(500)
  expensiveMethod() {}
}
```

上面代码一共使用了四个装饰器，一个用在类本身，另外三个用在类方法。它们不仅增加了代码的可读性，清晰地表达了意图，而且提供一种方便的手段，增加或修改类的功能。

### *Class*^类装饰器^

装饰器可以用来装饰整个类。

```
// lib.es5.d.ts
declare type ClassDecorator = <TFunction extends Function>
(
    target: TFunction
) => TFunction | void;
// 接收function类型，返回是function或void
```

基本上，装饰器的行为就是下面这样。

```
@decorator
class A {}

function decorator<FT extends Function>(target: FT): void | FT {}

// 等同于

class _A {}

var _A_Decorated = _decorator(_A) || _A;
function _decorator<FT extends Function>(target: FT): void | FT {}
```

:page_with_curl: *Example*

```
function decorator(target): void {
  (target as any).isTestable = true;
}

@decorator
class DecorativeClass {
  // ...
}

console.log((DecorativeClass as any).isTestable); // true
```

上面代码中，`@testable` 就是一个装饰器。它修改了 `MyTestableClass` 这个类的行为，为它加上了 静态*^static^* 属性 `isTestable` 。`testable` 函数的参数 `target` 是 `MyTestableClass` 类本身。

🧪 *Experimental*

可以为装饰器添加方法，此时返回 `ClassDecorator` 类型即可。

:memo: *Note*

实际上 `decorator('foo', 'bar')` 处就执行并传参 `'foo', 'bar'` 给了 `decorator` 函数，将返回的函数给 `@` ，而这个返回的函数符合 `type ClassDecorator` 的范式。可以理解为 *IIFE* 。

```
function decorator(...param): ClassDecorator {
  return target => {
    (target as any)[param[0]] = param[1];
  }
}

@decorator('foo', 'bar')
class ParamDecorativeClass {
  // ...
}

console.log((ParamDecorativeClass as any).foo);
// bar
```

也就是说，装饰器是一个对类进行处理的函数。装饰器函数*^decorate^* 的第一个参数，就是所要装饰的目标类。

:memo: *Note*装饰器对类的行为的改变，是代码 **编译** 时发生的，而不是在运行时。这意味着，装饰器能在编译阶段运行代码。也就是说，装饰器本质就是编译时执行的函数。

如果想添加实例属性，可以通过目标类的 `prototype` 对象操作。

:page_with_curl: *Example*

```
function decorator(target): void {
  target.prototype.isTestable = true;
}

@decorator
class DecorativeClass { }

let obj = new DecorativeClass();
console.log((obj as any).isTestable); // true
```

上面代码中，装饰器函数 `testable` 是在目标类的 `prototype` 对象上添加属性，因此就可以在实例上调用。

下面是另外一个例子。

:page_with_curl: *Example*

```
// mixins.js
export function mixins(...list) {
  return function (target) {
    Object.assign(target.prototype, ...list)
  }
}

// main.js
import { mixins } from './mixins.js'

const Foo = {
  foo() {
    console.log('foo')
  }
};

@mixins(Foo)
class MyClass {
}

let obj = new MyClass();
(obj as { foo() }).foo() // 'foo'
```

上面代码通过装饰器 `mixins` ，把 `Foo` 对象的方法添加到了 `MyClass` 的实例上面。没有装饰器 *@decorator* 时，可以用 `Object.assign()` 模拟这个功能。

```
const Foo = {
  foo() { console.log('foo') }
};

class MyClass { }

Object.assign(MyClass.prototype, Foo);

let obj = new MyClass();
obj.foo() // 'foo'
```

:memo: *Note*

实际开发中，*React* 与 *Redux* 库结合使用时，常常需要写成下面这样。

```
class MyReactComponent extends React.Component {}

export default connect(mapStateToProps, mapDispatchToProps)(MyReactComponent);
```

有了装饰器，就可以改写上面的代码。

```
@connect(mapStateToProps, mapDispatchToProps)
export default class MyReactComponent extends React.Component {}
```

相对来说，后一种写法看上去更容易理解。

### *Property*^属性装饰器^

```
// lib.es5.d.ts
declare type PropertyDecorator = (
    target: Object, // 被装饰的类
    propertyKey: string | symbol //被装饰类的属性名
) => void;
```

:exclamation:*Warning***不要使用：**

使用属性装饰器的时候，几乎没有作用，原因是装饰器的本意是要“装饰”类的 实例*^instance^* ，但是这个时候实例还没生成，所以只能去装饰 原型*^prototype^* ；由于无法直接在类的顶层创建直接修改原型的语句，因此会产生一个和实例同名的属性，从而原型上的属性会直接被实例上的属性覆盖。

```
class Class {
  @(decorator as PropertyDecorator)
  property: any;
}

function decorator(target: object, propertyKey: string | symbol): void {
  console.log(target === Class.prototype);
  // true
}
```

使用 方法装饰器*^method-decorator^* 的时候，由于方法是直接定义在 原型*^.prototype^* 上的，因此修改有效。

### *Method*^方法装饰器^

装饰器不仅可以装饰类，还可以装饰类的方法。

```
// lib.es5.d.ts
declare type MethodDecorator =
    <T>(
        target: // 被装饰的类
           Object,
        propertyKey: //被装饰类的方法名
           string | symbol,
        descriptor: // 属性描述符
           TypedPropertyDescriptor<T>
    )
        => TypedPropertyDescriptor<T> | void;
```

另外，上面代码说明，装饰器*^readonly^* 可以通过修改 描述对象*^descriptor^* 的值达到修改属性的方法*^method^* ，注意描述对象此时是存储在 原型链*^prototype^* 上的。

:page_with_curl: *Example*使用 *@decorator* 实现 *logger*

```
function log(target: Object, propertyKey: string, descriptor: PropertyDescriptor) {
  let originalMethod = descriptor.value;
  descriptor.value = function (...args: any[]) {
    console.log("wrapped function: before invoking " + propertyKey);
    let result = originalMethod.apply(this, args);
    console.log("wrapped function: after invoking " + propertyKey);
    return result;
  };
}

class Task {
  @(log as MethodDecorator)
  runTask(arg: any): any {
    console.log("runTask invoked, args: " + arg);
    return "finished";
  }
}

let task = new Task();
let result = task.runTask("learn ts");
console.log("result: " + result);


  // wrapped function: before invoking runTask
  // runTask invoked, args: learn ts
  // wrapped function: after invoking runTask
  // result: finished
```

:page_with_curl: *Example*使用 *Proxy* 实现 *logger*

*Proxy* 和 *@decorator* 区别：

1. *Proxy* 只能实现“眼前”，看不长远（要么代理 *function*，要么代理 *class*），不能同时代理
2. *@decorator* 可以通过 *target* 和 *propKey* 同时获得 *class* 和 *function*作为*prototype*被修改 ，以及通过 *descriptor* 获取 *function* 暴露的属性描述符，可以在运行之前通过 钩子*^hook^* 修改 值*^descriptor.value^* 插入

```
class Task {
  runTask(arg: any): string {
    console.log(`runTask invoked, args:${arg}`);
    return "finished";
  }
}

// log 通过Proxy的apply实现了@decorator的效果
// 区别是decorator是编译时就修改内容，而proxy要到运行时
const log = (targetFunction) => new Proxy(targetFunction, {
  apply<F extends Function>(target: F, thisArg: Object, argArray: Array<any>) {
    console.log("wrapped function: before invoking " + target.name);
    let result = Reflect.apply(target, thisArg, argArray);
    console.log("wrapped function: after invoking " + target.name);
    return result;
  }
});

let task = new Task();
let logFn = log(task.runTask);
let result = logFn('foo');
console.log("result: " + result);

// wrapped function: before invoking runTask
// runTask invoked, args:foo
// wrapped function: after invoking runTask
// result: finished
```

### *Parameter*^参数装饰器^

```
declare type ParameterDecorator = (
    target: // 被装饰的类
       Object,
    propertyKey: // 方法名
       string | symbol,
    parameterIndex: // 方法中参数的索引值
       number
) => void;
```

:exclamation:*Warning***不要使用：**

由于传入的三个参数 *target, key, parameterIndex* 都无法对形参进行实质性修改，且是最早运行的，因此非常鸡肋。

```
function Log(target: Function, key: string, parameterIndex: number):void {
  console.log(key);

  let functionLogged = key || target.prototype.constructor.name;
  console.log(`The parameter in position ${parameterIndex} at ${functionLogged} has been decorated`);
}

class Greeter {
  greeting: string;
  constructor(@(Log as ParameterDecorator) phrase: string)  {
    this.greeting = phrase;
  }
}
```

### *Usage*^应用^

装饰器有注释的作用。

:page_with_curl: *Example 1*

```
const testableList = new Set();
let testable = <TFunction extends Function>(target: TFunction): void => {
  testableList.add(target.name);
};

let readonly = <T>(target: Object, propertyKey: string | symbol, descriptor: TypedPropertyDescriptor<T>): void => {
  Reflect.defineProperty(target, propertyKey, {
    writable: false
  });
};

let nonEnumAble = <T>(target: Object, propertyKey: string | symbol, descriptor: TypedPropertyDescriptor<T>): void => {
  Reflect.defineProperty(target, propertyKey, {
    enumerable: false
  });
};

@(testable as ClassDecorator)
// @testable
class Person {
  #name
  @(readonly as MethodDecorator)
  @(nonEnumAble as MethodDecorator)
  // @readonly
  // @nonEnumAble
  name() {
    return this.#name;
  }
}

console.log([...testableList]); // [ 'Person' ]
console.log(Reflect.getOwnPropertyDescriptor(Person, 'name'));
// {
//   value: 'Person',
//   writable: false,
//   enumerable: false,
//   configurable: true
// }
```

从上面代码中，我们一眼就能看出，`Person` 类是可测试的，而 `name` 方法是只读和不可枚举的。

下面是使用 *Decorator* 写法的**组件**[6]，看上去一目了然。

```
@Component({
  tag: 'my-component',
  styleUrl: 'my-component.scss'
})
export class MyComponent {
  @Prop() first: string;
  @Prop() last: string;
  @State() isVisible: boolean = true;

  render() {
    return (
      <p>Hello, my name is {this.first} {this.last}</p>
    );
  }
}
```

如果同一个方法有多个装饰器，会像剥洋葱一样，先从外到内进入，然后由内向外执行。

```
function dec(id): MethodDecorator {
  console.log('evaluated', id);
  return function (target) {
    console.log('executed', id);
  }
}

class Example {
@dec(1)
@dec(2)
  method(){}
}

// evaluated 1
// evaluated 2
// executed 2
// executed 1
```

上面代码中，外层装饰器 `@dec(1)` 先进入，但是内层装饰器 `@dec(2)` 先执行。

## *Compile*^编译^

*TypeScript* 通过 `tsconfig.json` 修改编译选项，可以：

1. 用于标识 *TypeScript* 项目的根路径
2. 用于配置 *TypeScript* 编译器
3. 用于指定编译的文件

### *Field*^重要字段^

1. *files* - 设置要编译的文件的名称
2. *include* - 设置需要进行编译的文件，支持路径模式匹配
3. *exclude* - 设置无需进行编译的文件，支持路径模式匹配
4. *compilerOptions* - 设置与编译流程相关的选项

#### *CompilerOptions*^选项^

*compilerOptions* 支持很多选项，常见的有 `baseUrl`、 `target`、`baseUrl`、 `moduleResolution` 和 `lib` 等。

*compilerOptions* 每个选项的详细说明如下：

```
{
  "compilerOptions": {

    /* 基本选项 */
    "target": "es5",                       // 指定 ECMAScript 目标版本: 'ES3' (default), 'ES5', 'ES6'/'ES2015', 'ES2016', 'ES2017', or 'ESNEXT'
    "module": "commonjs",                  // 指定使用模块: 'commonjs', 'amd', 'system', 'umd' or 'es2015'
    "lib": [],                             // 指定要包含在编译中的库文件
    "allowJs": true,                       // 允许编译 javascript 文件
    "checkJs": true,                       // 报告 javascript 文件中的错误
    "jsx": "preserve",                     // 指定 jsx 代码的生成: 'preserve', 'react-native', or 'react'
    "declaration": true,                   // 生成相应的 '.d.ts' 文件
    "sourceMap": true,                     // 生成相应的 '.map' 文件
    "outFile": "./",                       // 将输出文件合并为一个文件
    "outDir": "./",                        // 指定输出目录
    "rootDir": "./",                       // 用来控制输出目录结构 --outDir.
    "removeComments": true,                // 删除编译后的所有的注释
    "noEmit": true,                        // 不生成输出文件
    "importHelpers": true,                 // 从 tslib 导入辅助工具函数
    "isolatedModules": true,               // 将每个文件做为单独的模块 （与 'ts.transpileModule' 类似）.

    /* 严格的类型检查选项 */
    "strict": true,                        // 启用所有严格类型检查选项
    "noImplicitAny": true,                 // 在表达式和声明上有隐含的 any类型时报错
    "strictNullChecks": true,              // 启用严格的 null 检查
    "noImplicitThis": true,                // 当 this 表达式值为 any 类型的时候，生成一个错误
    "alwaysStrict": true,                  // 以严格模式检查每个模块，并在每个文件里加入 'use strict'

    /* 额外的检查 */
    "noUnusedLocals": true,                // 有未使用的变量时，抛出错误
    "noUnusedParameters": true,            // 有未使用的参数时，抛出错误
    "noImplicitReturns": true,             // 并不是所有函数里的代码都有返回值时，抛出错误
    "noFallthroughCasesInSwitch": true,    // 报告 switch 语句的 fallthrough 错误。（即，不允许 switch 的 case 语句贯穿）

    /* 模块解析选项 */
    "moduleResolution": "node",            // 选择模块解析策略： 'node' (Node.js) or 'classic' (TypeScript pre-1.6)
    "baseUrl": "./",                       // 用于解析非相对模块名称的基目录
    "paths": {},                           // 模块名到基于 baseUrl 的路径映射的列表
    "rootDirs": [],                        // 根文件夹列表，其组合内容表示项目运行时的结构内容
    "typeRoots": [],                       // 包含类型声明的文件列表
    "types": [],                           // 需要包含的类型声明文件名列表
    "allowSyntheticDefaultImports": true,  // 允许从没有设置默认导出的模块中默认导入。

    /* Source Map Options */
    "sourceRoot": "./",                    // 指定调试器应该找到 TypeScript 文件而不是源文件的位置
    "mapRoot": "./",                       // 指定调试器应该找到映射文件而不是生成文件的位置
    "inlineSourceMap": true,               // 生成单个 soucemaps 文件，而不是将 sourcemaps 生成不同的文件
    "inlineSources": true,                 // 将代码与 sourcemaps 生成到一个文件中，要求同时设置了 --inlineSourceMap 或 --sourceMap 属性

    /* 其他选项 */
    "experimentalDecorators": true,        // 启用装饰器
    "emitDecoratorMetadata": true          // 为装饰器提供元数据的支持
  }
}
```

## *Module*^模块^

Solve - Cannot find module 'fs' Error in TypeScript | bobbyhadz

> ## Excerpt
>
> To solve the "Cannot find module `fs` or its corresponding type declarations" error, install the types for node by running the command `npm i -D @types/node`. You can then import `fs` with the following line of code `import * as fs from 'fs'`.

------

Solve - Cannot find module 'fs' Error in TypeScript **#**[7]

**To solve the "Cannot find module `fs` or its corresponding type declarations" error, install the types for node by running the command `npm i -D @types/node`. You can then import `fs` with the following line of code `import \* as fs from 'fs'`.**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/10MvibkFjuHGXDtziaRz7lo0cibJRIrt96SZib0u7LwOI5u09jqsN6gsLWzYRIAibgKzr5wbduX7m9pTe3dTgLCpxOA/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1)typescript cannot find module fs

Make sure to install the typings for node, by opening your terminal in your project's root directory and running the following command:

```
Copied!npm i -D @types/node
```

This will install the typings for node as a dev dependency in your project.

Now you are able to import the `fs` module with the following line of code.

```
Copied!import * as fs from 'fs';

console.log(fs);
```

If your error has not been resolved, open your `tsconfig.json` file and make sure the `types` array contains the string `node`.

```
Copied!{
  "compilerOptions": {
    "types": [
      "node"
    ]
  },
}
```

This should fix the error and now TypeScript should be able to find the type definitions for the `fs` module.

If the error is not resolved, try to delete your `node_modules` and `package-lock.json` files, re-run `npm install` and restart your IDE.

```
Copied!rm -rf node_modules package-lock.json

npm install
```

Make sure to restart your IDE if the error still persists. VSCode glitches often and a reboot solves things sometimes.

Here is an example of how you would read a file in the same directory named `another-file.ts` with the `fs` module using TypeScript.

```
Copied!import * as fs from 'fs';
import * as path from 'path';

console.log(
  fs.readFileSync(path.join(__dirname, './another-file.ts'), {
    encoding: 'utf-8',
  }),
);
```

And here is the output in my terminal showing the contents of `another-file.ts`.

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)fs reading file success

## *Tricks*^技巧^

### 在线工具

:link: *Href****TypeScript Playground\***[8]

*TypeScript* 官方提供的在线 *TypeScript* 运行环境，利用它你可以方便地学习 *TypeScript* 相关知识与不同版本的功能特性。

:link: *Href****TypeScript UML Playground\***[9]

一款在线 TypeScript UML 工具，利用它你可以为指定的 TypeScript 代码生成 UML 类图。

:link: *Href****JSON TO TS\***[10]

为指定的 *JSON* 数据生成对应的 *TypeScript* 接口定义。

:link: *Href****Schemats\***[11]

基于 *SQL* *^(Postgres,MySQL)^* 数据库中的 *schema* 字段自动生成 *TypeScript* 接口定义。

:link: *Href****TypeScript AST Viewer\***[12]

一款 *TypeScript AST* 在线工具，利用它你可以查看指定 *TypeScript* 代码对应的 *AST**Abstract Syntax Tree* 抽象语法树。

:link: *Href****TypeDoc\***[13]

*TypeDoc* 用于将 *TypeScript* 源代码中的注释转换为 *HTML* 文档或 *JSON* 模型。它可灵活扩展，并支持多种配置。

:link: *Href****TypeScript ESLint\***[14]

使用 *TypeScript ESLint (TSLint)* 可以帮助我们规范代码质量，提高团队开发效率。

### 完整性检查[15]

### 参考资料

[1]*TypeScript Playground*: *https://www.typescriptlang.org/play*[2]类型守卫*^guards^*: *#type-guards-ts*[3]*WeakMap()*: *#weakmap-as-private-before-es2022*[4]接口*^interface^*: *#interface-readonly-ts*[5]**重载***overload*: *#function-overload-ts*[6]组件: *https://github.com/ionic-team/stencil*[7]#: *https://bobbyhadz.com/blog/typescript-cannot-find-module-fs#solve---cannot-find-module-fs-error-in-typescript*[8]*TypeScript Playground*: *https://www.typescriptlang.org/play/*[9]*TypeScript UML Playground*: *https://tsuml-demo.firebaseapp.com/*[10]*JSON TO TS*: *https://www.jsontots.com*[11]*Schemats*: *https://github.com/SweetIQ/schemats*[12]*TypeScript AST Viewer*: *https://ts-ast-viewer.com*[13]*TypeDoc*: *https://typedoc.org*[14]*TypeScript ESLint*: *https://typescript-eslint.io*[15]完整性检查: *#type-wildcard-never-ts-comprehensive-inspection*



喜欢此内容的人还喜欢

501errors？？如何正确打开CODESYS的例程？

 

Hello工控

不喜欢

不看的原因

确定

- 内容质量低
- 不看此公众号

![img](https://mmbiz.qpic.cn/mmbiz_jpg/Fgj82EjZVIXfPUlUF3hmGauLpf6afUxS5lGo8kBA1FRDG4QfjyUGyEbapNU23yicv2PXibFZkhnuStNUxBFqAGRg/0?wx_fmt=jpeg)

学php培训去哪里好(PHP培训要学些什么)

 

码农素材

不喜欢

不看的原因

确定

- 内容质量低
- 不看此公众号

![img](https://mmbiz.qpic.cn/mmbiz_jpg/MIu0FhmCiaYZE0ibjx2gYnIPWPOf6EU4x0Y5LBf5S8TJX3Ia9LB2iaZfbCVic4q1icD6gSoiacicaq0eXE8TMZ2xdo9bw/0?wx_fmt=jpeg)

【宇聊】第3期：ChatGPT生成登录网页代码简析

 

小宇聊算法

不喜欢

不看的原因

确定

- 内容质量低
- 不看此公众号

![img](https://mmbiz.qpic.cn/sz_mmbiz_jpg/noZLg2Ju4u21PabbC4kZ2oPg6NpwJyRpOCNf0akTdmSa0dc7EaVsyF88VZK8TeaOMqt59h43eobsF8w9WxOcXw/0?wx_fmt=jpeg)

![img](https://mp.weixin.qq.com/mp/qrcode?scene=10000004&size=102&__biz=MzU4MTIzMjc4Ng==&mid=2247484974&idx=1&sn=11d079eeea728d45b70bc8ae40052f94&send_time=)

微信扫一扫
关注该公众号