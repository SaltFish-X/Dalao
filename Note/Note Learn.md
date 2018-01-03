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

```typescript
// 进行类型检查 含有label属性且类型为string的对象
interface LabelledValue {
  label: string
}

// 可选属性 ?:
// 用于可能存在的属性进行预定义，捕获引用不存在的属性导致的错误
interface SquareConfig {
  color?: string
  width?: number
  [propName: string]: any // 对象可存在其他属性，避免类型检查
}

// 只读属性 readonly 赋值后无法更改
// 属性用 readonly 变量用 const
interface Point {
  readonly x: number
  readonly y: number
}

/* 可索引类型 [index:] 描述对象索引的类型，索引返回值类型
 * 索引类型有数字和字符串两种，可同时使用。
 * 但是数字索引的返回值必须是字符串索引返回值类型的子类型
 * 因为使用number索引时，JavaScript会将其转为string再索引对象
 */
interface StringArray {
  [index: number]: string
}

// 错误：使用'string'索引，有时会得到Animal!
interface NotOkay {
  [x: number]: Animal;
  [x: string]: Dog; // Dog为Animal的子类
}

```

