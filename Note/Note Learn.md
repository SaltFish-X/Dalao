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

#### [Ts文档](https://www.tslang.cn/docs/handbook/basic-types.html)

#### ts配置文件 tsconfig.json

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

#### webpack 配置

`ts-loader`负责加载 `source-map-loader` 用来调试

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

  ​

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

