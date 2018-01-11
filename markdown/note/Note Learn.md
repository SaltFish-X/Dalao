# Note Learn

### Note Node

#### [关于Node.js的__dirname，__filename，process.cwd()，./文件路径的一些坑](https://segmentfault.com/a/1190000009368204)

```
__dirname: 总是返回被执行的 js 所在文件夹的绝对路径
__filename: 总是返回被执行的 js 的绝对路径
process.cwd(): 总是返回运行 node 命令时所在的文件夹的绝对路径
./: 跟 process.cwd() 一样，返回 node 命令时所在的文件夹的绝对路径

require(./)和__dirname 的效果相同
```

#### AMD, CMD, module.exports, export,CommonJS

```
AMD 提前执行（依赖前置）requireJs
CMD 延迟执行（依赖就近）seajs
ES6 Modules
```

#### Install mongodb

```
sudo mkdir -p /data/db
sudo chown -R $USER /data/db

rm /data/db/mongod.lock

这里有mongo和mongod两个命令
使用mongod命令先启动本地的mongo服务
```

#### 启动supervisor

```
supervisor --harmony index
```

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

