# Note Css

### 1px线

```css
// 上下两条 颜色偏蓝
box-shadow: 0 1px 1px -1px rgba(0, 0, 0, 0.5);

// 按需添加
li{
	position: relative;
	border:none;
}
li:after{
    content: '';
	position: absolute;
	left: 0;
	background: #000;
	width: 100%;
	height: 1px;
	transform: scaleY(0.5);
	transform-origin: 0 0;
}
```

### 四个半椭圆

```css
向上半椭圆
brouder-radius: 50%/100% 100% 0 0

向下半椭圆
brouder-radius: 50%/0 0 100% 100%

向左半椭圆
brouder-radius: 100% 0 0 100%/50%

向右半椭圆
brouder-radius: 0 100% 100% 0/50%
```

### **Selectors Level 3**

```css
子串匹配的属性选择器， E[attribute^="value"]， E[attribute$="value"]， E[attribute*="value"]

新的伪类：:target， :enabled 和 :disabled， :checked， :indeterminate， :root， :nth-child 和 :nth-last-child， :nth-of-type 和 :nth-last-of-type， :last-child， :first-of-type 和 :last-of-type， :only-child 和 :only-of-type， :empty， 和 :not。

伪元素使用两个冒号而不是一个来表示：:after 变为 ::after， :before 变为 ::before， :first-letter 变为 ::first-letter， 还有 :first-line 变为 ::first-line。

新的 general sibling combinator(普通兄弟选择器)  ( h1~pre )。
```

### inline-block使用

```
inline-block的父元素加font-size: 0
这样去掉空格和间隙
```

### 背景模糊

```css
filter:bulr(10px)
overflow:hidden
```

### 超出文字省略

```css
white-space：nowarp
overflow：hidden
text-overflow：ellipsis
```



## 布局

### [垂直居中](http://demo.doyoe.com/css/alignment/)

```
html结构
.main
  .element
  
1. margin负值 需要定高宽
.element{
  position: absolute;  
  left: 50%; 
  top: 50%; 
  width: 600px;   
  height: 40px;  
  margin-top: -20px;
  margin-left: -300px; 
}

2. vertical-align inline-block 需要设置父元素after 

.element{
  display: inline-block;
  vertical-align:middle;
}

.main{
  text-align:center;
}
.main:after{
  content:'';
  width:0;
  hegiht:100%;
  display:inline-block;
  vertical-align:middle;
}

3.transform 兼容到IE9
.element{
  position: relative;
  width: 200px;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}

4.flex
```

### table-cell

table-cell会引起重排影响性能，所以不建议使用

zoom可以引发 layout，但不引起页面差异。可以用来处理浏览器自作主张的优化。肉眼看不到效果，要看 performance 日志

### [瀑布流](https://www.w3cplus.com/css/pure-css-create-masonry-layout.html)

css的瀑布流均为多行文本的瀑布流，有局限性

#### Multi-columns 多栏布局 用于多行文本

[MDN相关文档](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Columns)

```scss
.contained {
    column-count:5; // 列数
    column-gap:0; // 列间距
    .item {
        // 控制堆栈间的空隙。将文本块分解成单独的列，以免项目列表的内容跨列
        break-inside: avoid; 
        box-sizing: border-box; // 避免中断布局
    }
}

```

#### flex

```scss
.contained {
    display: flex;
    flex-flow: column warp; //IE11正常，chrome40、Firefox34 bug
    height: 100px; // 必须设置
}

// 另一种
.contained {
    display:flex;
    flex-direction: row;
    .column {
        flex-direction: column;
    }
}
```

### 表单lable对齐

```
letter-spacing:2em 需要空几个字就几em，但是会让冒号也空出来

使用inline-block和text-align:justify
https://www.w3cplus.com/css/text-align-justify-and-rwd.html

text-align-last: justify;

text-align:justify 往里面塞内联<i></i>块逼成两行
或者上伪元素
div:after {
    content: " ";
    display: inline-block;
    width: 100%;
}
```

### [文字垂直居中](https://blog.csdn.net/maomaolaoshi/article/details/77949617)

```
vertical-align:middle; 一般用于行内的文字
vertical-align用来指定行内元素（inline）和行内块级元素（inline-block）或表格单元格（table-cell）元素的垂直对齐方式。

line-hegiht & hegiht
目标元素（字体）的line-height大小等于父类元素的height大小，可以实现垂直居中。 

行内块级元素垂直居中 & vertical-align：top
1. 更改字体所在的元素为display：inline-block，position：relative; 
2. 设置字体的line-height与font-size相等； 
3. 设置字体所在元素，top：50%;，vertical-align:top，margin-top为负的font-size大小的一半。
```

