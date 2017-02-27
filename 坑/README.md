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