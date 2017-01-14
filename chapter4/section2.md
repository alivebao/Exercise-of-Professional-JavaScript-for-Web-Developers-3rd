# 第二节 执行环境及作用域
1. 执行环境的作用是什么？  
  答：执行环境定义了变量/函数有权访问的其他数据，决定了他们各自的行为。每个执行环境都有一个与之关联的变量对象，环境中定义的所有变量和函数都保存在这个变量中。  
  每个函数都有自己的执行环境。当执行流进入一个函数时，函数的环境就会被压入一个环境栈中。函数执行完成栈再将该环境弹出，把控制全返回给之前的执行环境。  
  
2. 作用域链的作用是什么？  
  答：保证对执行环境有权访问的所有变量和函数的__有序访问__。作用域链的前端始终是__当前执行的代码所在环境的变量对象__。  
  作用域链中存放变量对象的顺序为：  
  当前执行代码所在环境的变量对象->外一层环境的变量对象->再外一层环境的变量对象->...->全局执行环境的变量对象。  
  标识符解析是沿着作用域链逐层搜索标识符的过程，搜索从前端开始逐级向后回溯，直到找到标识符位置。  
  
3. 分析以下代码的执行环境/作用域链
  ```
  var color = "blue";
  function changeColor() {
    var anotherColor = "red";
    
    function swapColors() {
        var tempColor = anotherColor;
        anotherColor = color;
        color = tempColor;
        //这里可以访问color/anotherColor/tempColor
    }
    //这里可以访问color/anotherColor
    swapColors();
  }
  //这里可以访问color
  changeColor();
  ```
  答：以上代码共涉及三个执行环境-全局环境、changeColor()局部环境和swapColors()局部环境。他们的执行环境间的关系和作用域链如下图所示。
  ![JavaScript组成部分](../../res/pic/4_2.png)  
  以该例中的swapColors()进行分析，其作用域包含三个对象，swapColors()本身的变量对象、changeColor()的的变量对象、全局的变量对象。在函数执行，搜索变量时，swapColors()会优先在自己的变量对象中进行搜索，搜索不到则在更外一层(changeColor)中进行搜索，直到搜索到变量为止。当搜索完全局环境仍无法找到变量时则报错。  
  
4. 以下代码打印的结果是？如果要在testFunction中使用外部的temp应如何操作？
```
var temp = "outer";
function testFunction() {
    var temp = "inner";
    console.log(temp); 
}
testFunction();         //inner
console.log(temp);      //outer
```
  答：打印结果见代码注释，在testFunction中想调用外部的temp时，可通过window.temp访问全局环境中的temp.