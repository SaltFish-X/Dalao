# Note Work

#### 装饰器

```
作用于类、类属性
增加新行为但不修改函数
```
#### jQuery绑定函数

```javascript
$.fn.func = func
```
#### bootStrap的栅栏

```css
.container {
  width: 100%;
}

.row:before,
.row:after {
  content: "";
  height: 0;
  clear: both;
  display: block;
}

/* 设置padding会把元素挤下去*/
[class*='col-'] {
  float: left;
  min-height: 1px;
  /*padding: 10px;*/ 
}

.col-i {
  width: 100 / 12 * 1 %;
}
```
#### [HTML标签标准](https://www.w3.org/TR/html5/dom.html#kinds-of-content)

#### vue的图片

```javascript 
img: require('../') //正常的路径加require
background-image: url('path/to/your/source') // css的路径
```
#### commit设定时间

```
git commit --amend --date=2017-10-08T09:51:07
```
#### vueRouter lazy-loading

```
v3.0.1
const Foo = () => Promise.resolve({ /* 组件定义对象 */ })
import('./Foo.vue') // 返回 Promise

const Foo = () => import('./Foo.vue')

把组件按组分块

有时候我们想把某个路由下的所有组件都打包在同个异步块 (chunk) 中。只需要使用 命名 chunk，一个特殊的注释语法来提供 chunk name (需要 Webpack > 2.4)。

const Foo = () => import(/* webpackChunkName: "group-foo" */ './Foo.vue')
const Bar = () => import(/* webpackChunkName: "group-foo" */ './Bar.vue')
const Baz = () => import(/* webpackChunkName: "group-foo" */ './Baz.vue')
```

```
v2.1.1
const Foo = resolve => require(['./Foo.vue'], resolve) //AMD风格

把组件按组分块

有时候我们想把某个路由下的所有组件都打包在同个异步 chunk 中。只需要 给 chunk 命名，提供 `require.ensure` 第三个参数作为 chunk 的名称:

const Foo = r => require.ensure([], () => r(require('./Foo.vue')), 'group-foo')
const Bar = r => require.ensure([], () => r(require('./Bar.vue')), 'group-foo')
const Baz = r => require.ensure([], () => r(require('./Baz.vue')), 'group-foo')
```
#### 符号!!~

```
~为取反运算符，如果names.indexOf(name)返回值为-1，即names不包含name，那么~-1 = 0。其他值取反后值都不为0。结合!~来判断names是否包含name

!!name 用来判断name是否为空字符或undefined 

arrary.prototype.indexof ， 没有包含，就返回-1

～是位运算，按位取反。效果是转number，+1，然后取负数。
也就是说，如果不包含得到-1，就+1，再乘以-1，也就是0

!! 就是强转boolean
把 0 换成 false
!! 在if里面一般是可以省略的

!!~roles.indexOf(1)
```



#### vue 父子组件 属性通讯简写法

```
:visible.sync="visible"
拆成 可关闭el-dialog
:visible="visible"
@update:visible="val => $emit('update:visible', val)"
```

