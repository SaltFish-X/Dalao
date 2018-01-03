# Note Css

## [Flex语法](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

### 基本概念

```
flex container “容器” 采用flex布局的元素 
flex item “项目” 采用flex布局的元素的子元素
main axis 水平主轴 main start 主轴开始位置 main end 主轴结束位置
cross axis 垂直交叉轴 cross start 开始位置 cross end 结束位置
main size 项目所占主轴空间 cross size 项目所占交叉轴空间f![flex布局001]
```

![flex布局001](../img/flex布局001.png)



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

| align-item  | 交叉轴的对齐方式              |
| ----------- | --------------------- |
| flex-start  | 交叉轴起点对齐               |
| flex-end    | 交叉轴终点对齐               |
| center      | 交叉轴中点对齐               |
| baseline    | 第一行文字的基线对齐            |
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

## 小技巧

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

## 布局

### 垂直居中

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

.wrap{
  text-align:center;
}
.wrap:after{
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
```

