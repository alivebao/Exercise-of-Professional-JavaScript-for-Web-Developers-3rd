# 第四章 变量、作用域和内存问题

## 1. 基本类型和引用类型的值  
  1. JS的5种基本类型是？  
  2. 什么是引用类型，和基本类型的区别是什么？  
  3. 引用类型和基本类型的区别？  
  4. 向函数传参的过程中，对于引用类型是按值传递还是按引用传递？如何证明?
  5. typeof是用于检测String/Number/Boolean/Undefined的有效工具，但对null或对象，typeof均会返回"object"。应如何确定某对象是什么类型的？  

## 2. 执行环境及作用域  
  1. 执行环境的作用是什么？  
  2. 作用域链的作用是什么？  
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