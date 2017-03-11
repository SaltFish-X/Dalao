# 工作中的坑

[TOC]

## 1.&&运算符

```javascript
var ob = new Boolean(false)
console.info( ob && true) // true
console.info( true && ob ) // Boolean {[[PrimitiveValue]]: false}
```

原因：
```javascript
a1 && a2 如果 a1能转换为flase则返回a1，否则返回 a2

var ob = new Boolean(false)
Boolean(ob) // true 不能 new Boolean
ob.valueOf() // false
```

## 2.base64换行
```
base64每76个字符换行，window和linux下的换行符不一样，会导致错误
```

## 3.append VS += VS join
[测速度的网站,代码自定义](http://jsben.ch/#/TWq40)
[测速度的网站，别人写好的样式](https://jsperf.com/jquery-append-vs-html-list-performance/24)

```
最终结果是 +=有两种写法 
element.innerHTML += lement.innerHTML + ''

html += html + ''
element.innerHTML = html

后者更快，和join差不多，甚至快于join
```

## 4.window.name

```javascript
var name = function{}
name // "function (){}"
```

原因：
```
name的全局变量被视作window.name
return String
```