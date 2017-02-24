# 每日一题（也称大佬带我装逼带我飞）

[1. 这家前后端关系肯定好不到哪里去 出题人 B大](#1-这家前后端关系肯定好不到哪里去-出题人-b大)

[2. 这道算法题可以进leetcode 出题人 Y腿](#2-这道算法题可以进leetcode-出题人-y腿)

[3. 柯里化并不是那么容易 出题人 OlafCheng](#3-柯里化并不是那么容易-出题人-OlafCheng) 

[4. 三题全家桶 出题人 斌 ](#4-三题全家桶-出题人-斌)

### 1. 这家前后端关系肯定好不到哪里去 出题人 B大

这段php代码 可能输出一个 JSON 也可能输出空

```php
const foo = {
  bar: <?php>
}
```

输出json时示例如下

```php
const foo = {
  bar: {}
}
```

输出空的时示例如下

```php
const foo = {
  bar: 
}
```
很明显，输出空的时候会抛出异常，请问如何从js语法层面上解决这个问题

注：为防止XSS，应该避免使用eval和new Function

错误答案
```
1. ||
2. 三元
3. Object.assign({}, <%php%>) 因为不能保证这个JSON里没有引号，也不能保证没有反引号
4. escape escape传对象进去，会变成[Object object]
5. JSON.stringify() 
6. try catch 会报错……
```

思路：
```
JS语法中哪里可以不填东西，一个是Array 一个是函数的参数
```

正确答案：
```
1. [<%php%>][0]
2. (x => x)(<?php>)
```

欢乐吐槽时间：
```
Chobits：这样写代码的公司，前后端关系肯定好不到哪里去
小窝子：最好的解决办法不是叫后端输出个东西出来咩
一位乘客突然失去了梦想：这就是后端的锅
```

### 2. 这道算法题可以进leetcode 出题人 Y腿

已知一个字符串 aoobcooobaocoo，求包含abc（不限制顺序）的最小片段，这个字符串的片段为baoc

错误思路：
```
1. 正则 因为正则没有办法限制abc各出现一次
```

正确思路：
```
1. 将abc的索引值存入三个数组
2. 从三个数组中各取一个值，最大值和最小值相减记为cut，求cut最小值，并输出取出的三个值的索引。例：
var a,b,c,cut,index
a=[0,1,4,7,11]
b=[2,6,9,12]
c=[8,15,17]
cut = 2  index=[3,2,0]
3. 写出合适的算法
难点也在于写出合适的算法
```

算法思路：
```
1. 找相邻最近的ab ac bc各一个，然后取这三个值里的最大值，就是cut。最大值的两个点就是需要的index其中两个，b存不存在于剩下两组中需要笔头证明一下
2. 比如全排列一次 … 然后取其中的每种情况的最优解，因为数组里的数字本身是有序的，所以最多只需要遍历 xn 次，对 abc 的坐标数组顺序全排列一次，然后每种情况取一个递增序列，因为只要找到递增，就是这个情况的最优解了，所以 6 次查找也是 6*k*n = n …
```

### 3. 柯里化并不是那么容易 出题人 OlafCheng

实现如下函数：

```javascript
add(2,5) // 7
add(2)(5) // 7
```

思路：

```javascript
[].slice.call.(arguments).length
```

错误答案：

```javascript
function add() {
  function calculate() {
    var arr = [].slice.call(arguments);
    switch(arr.length) {
      case 0:
        return 0;
      case 1:
        return arr[0];
      default:
        return arr.reduce(function(ac, cv) {
          return ac + cv;
        })
    }
  }
  var result = calculate(arguments); // 这样写是错误的
  function func() {
    result += calculate(arguments);
    return func;
  }

  func.toString = func.valueOf = function() {
    return result;
  }

  return func;
}
```

出错原因：

```javascript
出错的原因是, arguments 是 array-like，不是 array
内部细节，直接当做实参传的话，会调用它的 toString 属性，转换成'[object Arguments]'
然后传进去的参数就不是数组或者 arguments 本身了，而是一个字符串
进行如下修改即可

var result = calculate.apply(null, arguments);
function func() {
  result += calculate.apply(null, arguments);
  return func;
}
```
正确答案：

```javascript
var tmp = function () {
            sum += Array.prototype.slice.call(arguments).reduce((a, b) => a + b, 0);
            return tmp;
          }


```

```javascript
const add = (...args) => {
  const calculate = (arr) => {
    return arr.length === 0 ? 0 : arr.length === 1 ? arr[0] : arr.reduce((ac, cv) => ac + cv);
  }

  let result = calculate(args);
  const func = (...args) => {
    result += calculate(args);
    return func;
  }

  func.toString = func.valueOf = () => result;

  return func;
}
```

### 4. 三题全家桶 出题人 斌 

1. 有如下HTML
    ```
    <ul>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
    </ul>

      实现以下要求
      1. 点击 ul 所有li的数量
      2. 点击 ul 当前li的值
      3. 不用框架
    ```

2. 垂直居中的方法越多越好

3. lazyman

思路：

第一题
```
ul.children.length
```

第二题
```
1.line-height
2.0宽元素 inline-block
3.伪元素inline-block
4.translate -50%/-50% + absolute 50%/50%
5.absolute offset 0/0/0/0
6.table-cell
7.flex
8.table + writing mode
```
第三题

```
自己Google LazyMan js
```
