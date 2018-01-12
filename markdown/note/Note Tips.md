# Note Tips

#### dirname，filename

[关于Node.js的__dirname，__filename，process.cwd()，./文件路径的一些坑](https://segmentfault.com/a/1190000009368204)

```
__dirname: 总是返回被执行的 js 所在文件夹的绝对路径
__filename: 总是返回被执行的 js 的绝对路径
process.cwd(): 总是返回运行 node 命令时所在的文件夹的绝对路径
./: 跟 process.cwd() 一样，返回 node 命令时所在的文件夹的绝对路径

require(./)和__dirname 的效果相同
```

#### AMD, CMD,UMD,CommonJS

##### CommonJS

node采用此规范， [CommonJs Wiki](https://en.wikipedia.org/wiki/CommonJS)本身是同步的

```
require()用来引入外部模块；
exports对象用于导出当前模块的方法或变量，唯一的导出口；
module对象就代表模块本身。
```

##### AMD

RequireJS采用此规范 [AMD规范中文版](https://github.com/amdjs/amdjs-api/wiki/AMD-(%E4%B8%AD%E6%96%87%E7%89%88))

define(id?,dependencies?,factory)

```
id: 模块标识，可以省略。
dependencies: 所依赖的模块，可以省略。
factory: 模块的实现，或者一个JavaScript对象。    
```

##### CMD

seajs采用此规范  特点为延迟加载，就近依赖。（然而似乎已经没人维护了）

CMD 与 AMD 二者区别如下：

- 对于依赖的模块 CMD 是延迟执行，而 AMD 是提前执行（不过 RequireJS 从 2.0 开始，也改成可以延迟执行。 ）
- CMD 推崇 as lazy as possible（依赖就近），AMD 推崇依赖前置。
- AMD 的 api 默认是一个当多个用，CMD 严格的区分推崇职责单一，其每个 API 都简单纯粹。例如：AMD 里 require 分全局的和局部的。CMD 里面没有全局的 require，提供 seajs.use() 来实现模块系统的加载启动。

##### UMD

通用模块规范兼容AMD和CommonJS

##### ES6

ES6 模块与 CommonJS 模块的差异

- CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。
- CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。

[export规范](http://www.ecma-international.org/ecma-262/6.0/#sec-exports)

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

### 