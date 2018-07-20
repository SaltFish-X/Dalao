# Note Learn

## [Flex语法](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

### 基本概念

```
flex container “容器” 采用flex布局的元素 
flex item “项目” 采用flex布局的元素的子元素
main axis 水平主轴 main start 主轴开始位置 main end 主轴结束位置
cross axis 垂直交叉轴 cross start 开始位置 cross end 结束位置
main size 项目所占主轴空间 cross size 项目所占交叉轴空间f![flex布局001]
```

![flex布局001](../../img/flex布局001.png)



### flex container

```
flex-dircetion 主轴的方向
flex-wrap 主轴的换行
flex-flow: <flew-dircetion> || <flex-wrap> 简写

justify-content 主轴的对齐方式
align-items 交叉轴的对齐方式
align-content 多根轴线的对齐方式，只有一根轴线则属性无效
```

| flex-direction | 主轴的方向         |
| :------------- | ------------- |
| row            | 主轴为水平方向，起点在左侧 |
| row-reverse    | 主轴为水平方向，起点在右侧 |
| column         | 主轴为垂直方向，起点在上侧 |
| column-reverse | 主轴为垂直方向，起点在下侧 |

| flex-wrap    | 主轴的换行    |
| ------------ | -------- |
| nowrap 默认值   | 不换行      |
| wrap         | 换行，第一行在上 |
| wrap-reverse | 换行，第一行在下 |

| justify-content | 主轴的对齐方式       |
| --------------- | ------------- |
| flex-start 默认值  | 左对齐           |
| flex-end        | 右对齐           |
| center          | 居中            |
| space-between   | 两端对齐，item间隔相等 |
| space-around    | item两侧间隔相等    |

| align-items    | 交叉轴的对齐方式                       |
| -------------- | -------------------------------------- |
| flex-start     | 交叉轴起点对齐                         |
| flex-end       | 交叉轴终点对齐                         |
| center         | 交叉轴中点对齐                         |
| baseline       | 第一行文字的基线对齐                   |
| stretch 默认值 | 高度未设置或auto，将占满整个容器的高度 |

| align-content | 多根轴线的对齐方式             |
| ------------- | --------------------- |
| flex-start    | 交叉轴起点对齐               |
| flex-end      | 交叉轴终点对齐               |
| center        | 交叉轴中点对齐               |
| space-between | 交叉轴两端对齐，item间隔相等      |
| space-around  | item两侧间隔相等            |
| stretch 默认值   | 高度未设置或auto，将占满整个容器的高度 |

### flex item

```
order item排列顺序
flex-grow item放大比例
flex-shrink item缩小比例
flex-basis item初始大小
flex 缩写
align-self item对齐方式 覆盖align-item

order: <integer> 
item排列顺序 从小到大 默认为0

flex-grow: <number> 
item放大比例 默认为0（存在剩余空间也不放大）
如果所有item的flex-grow为1，将等分剩余空间
如果某个item的flex-grow为2，将比其他item所占据的剩余空间大一倍

flex-shrink: <number> 
item缩小比例 默认为1（空间不足则缩小）
如果某个item的flex-shrink为0，其他为1。则空间不足时，前者不缩小

flex-basis: <'width'> | auto
the initial main size of a flex item 主轴上的初始大小
<'width'>可以取以px、mm、pt结尾的绝对值，或百分数（相对于flex container的宽或高，取决于主轴方向）

Defined as a number followed by an absolute unit such as px, mm or pt, or a percentage of the parent flex container main size property. Negative values are invalid.

flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
auto 自适应 会伸长和缩短
元素会根据自身的宽度与高度来确定尺寸，但是会自行伸长以吸收flex容器中额外的自由空间，也会缩短至自身最小尺寸以适应容器。
这相当于将属性设置为 "flex: 1 1 auto".

initial 默认值 只缩短不伸长
属性默认值， 元素会根据自身宽高设置尺寸。它会缩短自身以适应容器，但不会伸长并吸收flex容器中的额外自由空间来适应容器 。
相当于将属性设置为"flex: 0 1 auto"。

none 非弹性
元素会根据自身宽高来设置尺寸。它是完全非弹性的：既不会缩短，也不会伸长来适应flex容器。
相当于将属性设置为"flex: 0 0 auto"。

align-self:auto | flex-start | flex-end | center | baseline | stretch 属性同align-item
会对齐当前 flex 行中的 flex 元素，并覆盖 align-items 的值. 如果任何 flex 元素的侧轴方向 margin 值设置为 auto，则会忽略 align-self。
```

### 参考文档

[**mdn文档**](https://developer.mozilla.org/en-US/docs/Web/CSS/flex)

[**A Complete Guide to Flexbox**](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

[**Flex 布局教程：实例篇**](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)

### Note TypeScript

#### Ts配置

##### tsconfig.json

```json
{
  "compilerOptions": {
    "outDir": "./built", //生成的所有文件放在built目录下 
    "allowJs": true, // 接受JavaScript做为输入
    "target": "es5" // 将JavaScript代码降级到低版本
  },
  // include 读取所有可识别的src目录下的文件
  "include": [
     "./src/**/*"
  ]
}
```

##### webpack 配置

`ts-loader`负责加载 `source-map-loader` 用来调试

##### 编译配置

```
在处理模块时，ts支持多种加载方式，需要使用不同的指令来区分。
Node.js(CommonJs): tsc --module commonjs Test.ts
Require.js(AMD): --moudule amd
```

##### [Ts文档](https://www.tslang.cn/docs/handbook/basic-types.html) 

跳过的章节：类型推论、类型兼容性

#### Ts 接口语法

##### 属性类型

```typescript
interface LabelledValue {
  label: string // 进行类型检查 含有label属性且类型为string的对象
}
```
##### 可选属性

预定义可能存在的属性，捕获引用不存在的属性导致的错误

 ```typescript
interface SquareConfig {
  color?: string
  width?: number
}

// 不存在的属性colour会报错
let mySquare = createSquare({ colour: "red", width: 100 })

解决方法
1. 接口加入任意数量的其他属性 [propName: string]: any 
2. 使用类型断言 { width: 100, opacity: 0.5 } as SquareConfig
3. 将这个对象赋值给一个另一个变量，跳过检查
4. 最佳方式是添加一个字符串索引签名
 ```

##### 函数类型

```typescript
interface SearchFunc {
  (source: string, subString: string): boolean
}
```

##### 只读属性 

* 属性用 readonly ，变量用 const

 ```typescript
// 赋值后无法更改
interface Point {
  readonly x: number
  readonly y: number
}
 ```

##### 可索引类型

 * 描述对象索引的类型，索引返回值类型。索引类型有数字和字符串两种，可同时使用
 * 但是数字索引的返回值必须是字符串索引返回值类型的子类型，因为使用number索引时，JavaScript会将其转为string再索引对象

 ```typescript
interface StringArray {
  [index: number]: string
}

// 错误：使用'string'索引，有时会得到Animal!
interface NotOkay {
  [x: number]: Animal;
  [x: string]: Dog  // Dog为Animal的子类
}
 ```

* 字符串索引签名

```typescript
interface NumberDictionary {
  [index: string]: number
  length: number   // 可以，length是number类型
  name: string     // 错误，`name`的类型与索引类型返回值的类型不匹配
}
```

##### 类类型

在接口中定义方法，在类中实现

 ```typescript
interface ClockInterface {
  currentTime: Date
  setTime(d: Date)
  // 定义构造器会报错，因为类型检查只对实例部分，constructor为静态部分
  new (hour: number, minute: number) 
}

class Clock implements ClockInterface {
  currentTime: Date;
  setTime(d: Date) {
      this.currentTime = d;
  }
  constructor(h: number, m: number) {}
}
 ```

一定要检查构造器的话，定义构造函数和实例方法的两个接口，和一个构造函数

```typescript
interface ClockConstructor {
    new (hour: number, minute: number): ClockInterface;
}

interface ClockInterface {
    tick();
}

function createClock(ctor: ClockConstructor, hour: number, minute: number): ClockInterface {
    return new ctor(hour, minute);
}

class DigitalClock implements ClockInterface {
    constructor(h: number, m: number) { }
    tick() {
        console.log("beep beep");
    }
}
```


接口也可以相互继承

```typescript
interface Square extends Shape, PenStroke {
  sideLength: number
}
```

##### 类的名词

```
静态变量：存在于类本身，用类名访问
实例变量：存在于实例上，需要new才能初始化。类中用this访问
抽象类：abstract 类似接口，抽象方法必须在派生类中实现
```

##### 范型

支持多种数据

[范型约束示例](https://www.tslang.cn/docs/handbook/generics.html)

```typescript
/* 范型函数
 * 使用类型变量<T>
 * 范型T捕获参数的类型，使函数能传入并返回数值类型
 */
function identity<T>(arg: T): T { return arg }

// type of output will be 'string'
let output = identity("myString");  
let output = identity<string>("myString"); 

/* 范型变量
 * 想以数组的数据格式操作<T>
 */
function identity<T>(arg: T[]): T[]
function identity<T>(arg: Array[]): T[]

// 还可以写成范型函数，范型接口，范型类，范型只能用于类的实例部分

```

##### 枚举

枚举成员具有一个数字值，它可以是常数或是计算得出的值，当满足如下条件时，枚举成员被当作是常数：

- 不具有初始化函数并且之前的枚举成员是常数。 在这种情况下，当前枚举成员的值为上一个枚举成员的值加1。 但第一个枚举元素是个例外。 如果它没有初始化方法，那么它的初始值为 0。
- 枚举成员使用`常数枚举表达式`初始化。 常数枚举表达式是TypeScript表达式的子集，它可以在编译阶段求值。 当一个表达式满足下面条件之一时，它就是一个常数枚举表达式：
  - 数字字面量
  - 引用之前定义的常数枚举成员（可以是在不同的枚举类型中定义的） 如果这个成员是在同一个枚举类型中定义的，可以使用非限定名来引用。
  - 带括号的常数枚举表达式
  - `+`, `-`, `~` 一元运算符应用于常数枚举表达式
  - `+`, `-`, `*`, `/`, `%`, `<<`, `>>`, `>>>`, `&`, `|`, `^`二元运算符，常数枚举表达式做为其一个操作对象。若常数枚举表达式求值后为 `NaN`或`Infinity`，则会在编译阶段报错。

所有其它情况的枚举成员被当作是需要计算得出的值。



枚举类型包含双向映射，为避免生成多余代码和间接引用，可使用常数枚举

```typescript
enum Enum {
    A
}
let a = Enum.A;
let nameOfA = Enum[a];

// 编译
var Enum;
(function (Enum) {
  Enum[Enum["A"] = 0] = "A";
})(Enum || (Enum = {}));
var a = Enum.A;
var nameOfA = Enum[a]; // "A"

const enum Enum {} // 常数枚举 不同于常规的枚举将在编译阶段删除
declare enum Enum {} // 外部枚举 描述已经存在的枚举类型
```

##### 高级类型

| 类型   |                                          |
| ---- | ---------------------------------------- |
| 交叉类型 | 将多个类型合并为一个类型 ，例：Person & Sercializable<br />该类型的对象同时拥有了这三种类型的成员 |
| 联合类型 | 值为多种类型之一，例子：number \| string<br />只能访问联合中共有的类方法 |
| 类型保护 | 定义函数的返回值为 *类型谓词*  确保运行时作用域的类型            |
| 待添加  |                                          |

```typescript
// 类型保护示例
// 必须用类型断言才能将两张类区别
if ((<Fish>pet).swim) {
    (<Fish>pet).swim();
}
else {
    (<Bird>pet).fly();
}

// 类型保护区分两种类
function isFish(pet: Fish | Bird): pet is Fish {
    return (<Fish>pet).swim !== undefined;
}

if (isFish(pet)) {
    pet.swim();
} else {
    pet.fly();
}

// instanceof类型保护
// instanceof的右侧要求是一个构造函数
if (padder instanceof SpaceRepeatingPadder) {
    padder; // 类型细化为'SpaceRepeatingPadder'
}
```

##### 模块 

* 可选模块加载

```typescript
import id = require('...') // 模块动态调用 

declare function require(moduleName: string): any;
import { ZipCodeValidator as Zip } from "./ZipCodeValidator";

if (needZipValidation) {
  let ZipCodeValidator: typeof Zip = require("./ZipCodeValidator");
    let validator = new ZipCodeValidator();
    if (validator.isAcceptable("...")) { /* ... */ }
}
```

外部模块

```typescript
declare module "url" {
    export interface Url {
        protocol?: string;
        hostname?: string;
        pathname?: string;
    }

    export function parse(urlStr: string, parseQueryString?, slashesDenoteHost?): Url;
}

declare module "path" {
    export function normalize(p: string): string;
    export function join(...paths: any[]): string;
    export let sep: string;
}
```

##### Mixins

先要混合的类，定义接口占位属性，最后用函数混合

```typescript
class Disposable {}
class Activatable {}

class SmartObject implements Disposable, Activatable {}
applyMixins(SmartObject, [Disposable, Activatable])

function applyMixins(derivedCtor: any, baseCtors: any[]) {
    baseCtors.forEach(baseCtor => {
        Object.getOwnPropertyNames(baseCtor.prototype).forEach(
          name => {
            derivedCtor.prototype[name] = baseCtor.prototype[name];
        });
    });
}
```



##### 命名空间 TODO

##### 装饰器TODO