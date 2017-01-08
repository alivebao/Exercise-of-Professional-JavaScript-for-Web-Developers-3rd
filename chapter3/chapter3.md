# 第三章 基本概念

## 1. 语法
  1. JS中的注释风格  
    答：包括单行注释和块级注释  
    ```
    //单行注释，只有一行
    /*
    块级注释，多行
    */
    ```
  2. 什么是严苛模式(strict mode)？如何启用?      答：严苛模式是为JS定义的一种不同的解析与执行模型，ECMAScipt在该模式下的一些不确定行为会得到处理，且某些不安全的行为也会抛出错误。  
    要在整个脚本中使用严苛模式，可以在脚本顶部添加：
    ```
    "use strict";
    ```
    要指定某个函数使用严苛模式，可以在函数内部的第一行包含该指令：
    ```
    function doSomething(){
        "use strict";
        ...
    }
    ```
    
## 2. 变量  
  定义变量时，使用var定义的变量与直接定义的变量有什么区别?  
    答：用var操作符定义的变量将成为定义该变量的作用域中的局部变量。  
    也就是说，若在函数站使用var定义一个变量，该变量在函数退出后就会被销毁。若不使用var而直接定义变量，则该变量为全局变量(不推荐，且在严苛模式下会抛出错误Uncaught ReferenceError: XX is not defined)
    
## 3. 数据类型
  1. JS的5种简单数据类型分别是？  
    答：Undefined/Null/Boolean/Number/String，此外还有一种复杂数据类型-Object(本质是由一组无序的键值对组成)  
  2. typeof的作用是？  
    答：负责检测给定变量的数据类型，使用方式为：
    ```
    var message = "aaa";
    console.log(typeof message); //"string"
    console.log(typeof(message));//"string"
    ```
    返回值一个字符串，可能的返回结果包括
      * "undefined" - 给定值未定义
      * "boolean" - 给定值为布尔值
      * "string" - 给定值为字符串
      * "number" - 给定值为数值
      * "object" - 给定值是对象或__null__
      * "function" - 给定值是函数
      
    __这里有个很奇怪的地方，可以对未声明的变量使用typeof判断类型，此时不会报错，会返回undefined__  
  3. 什么是Undefined类型？
    答：Undefeined类型只有一个值-undefined。使用var声明变量但未对其进行定义时，该变量的值即为undefined。此外，显式将变量定义为undefeined(var b = undefined)是没有必要的，这么做和直接定义一个变量(var a)是一样的效果。例：
    ```
    var a;
    console.log(a == undefined);    //true
    console.log(a);                 //undefined
    console.log(typeof a)           //undefined
    var b = undefined;
    console.log(a == b)             //true
    ```
  4. 什么是Null类型？  
    答：Null类型是第二个只有一个值的数据类型，其值为null。从逻辑的角度看，null值表示一个空对象指针(所以typeof检测null值时会返回"object")
    ```
    var car = null;
    console.log(typeof car);
    ```  
  5. Undefined和Null的关系？  
    答：undefined派生自null值，因此以下代码会返回true
    ```
    console.log(null == undefined) //true
    ```
    undefined主要用于表明一个值尚未定义。null用于强调该值是__空__的。  
    __只要意在保存对象的变量还没真正保存对象时，就应该明确的让该变量保存null__。
    
    