# Note

1. jQuery绑定函数

  ```javascript
  $.fn.func = func
  ```

2. bootStrap的栅栏
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
3. [HTML标签标准](https://www.w3.org/TR/html5/dom.html#kinds-of-content)

4. vue的图片

  ```javascript 
  img: require('../') //正常的路径加require
  background-image: url('path/to/your/source') // css的路径
  ```
  