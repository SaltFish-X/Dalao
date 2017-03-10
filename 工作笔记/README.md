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
