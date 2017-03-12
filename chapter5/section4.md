# 第四节 基本包装类型
1. 什么是基本包装类型，其意义何在？  
  答：ES5提供了3个特殊引用类型-Boolean/Number/String。  
    ```
    var s1 = "text";
    var s2 = s1.substring(2);
    ```
  基本类型不是对象，理论上来说不应该有方法，s1.substring是不正常的，而基本包装类型就是为了实现以上直观操作而存在的。
  为了实现这种操作，系统在后台自动完成了一系列处理：  
  1. 创建一个String类型的实例  
  2. 在实例上调用指定的方法  
  3. 销毁该实例  
2. 基本包装类型和引用类型主要有什么区别？  
  答：对象的生存期不同。  
  使用new操作法创建的引用类型的实例，在离开当前作用域之前一直保存在内存中。  
  自动创建的基本包类型对象只存在与一行代码执行的瞬间，然后立即被销毁。  
    ```
    var s = "text";
    s.color = "red";
    console.log(s.color);   //undefined
    ```  
  这里打印的结果为undefined，因为第二行创建的String对象在执行第三行代码时已经被销毁了，第三行代码又创建自己的String对象，而该对象没有color属性，因此会打印undefined。

3. 使用new调用基本包装类型的构造函数与直接调用同名的转型函数有何不同？  
  答：类型不同。  
    ```
    var value = "25";
    var number = Number(value);
    console.log(typeof number); //"number"
    
    var obj = new Number(value);
    console.log(typeof obj);    //"object"
    ```  
    
4. 下列代码的返回结果是？  
    ```
    var falseObj = new Boolean(false);
    var result = falseObj && true;
    console.log(result);
    ```    
  答：返回true。虽然falseObj的值是false，但他实际上是一个对象，布尔表达式中的所有对象都会被转化为true。  
  可通过falseObj.valueOf()获取其值false。一定要注意理解__基本类型的布尔值__与__Boolean对象__之间的区别(最好永远不要使用Boolean对象)。  
  
5. 介绍String类型中substring、substr和slice的用法？  
  答：substring和slice用法相同。substring和substr的区别为：  
  1. String.substring(beginIndex [,endIndex]]);  
  2. String.substr(beginIndex [, length]);  
  
  __三个函数均不会修改函数本身的值__，而是返回一个新的字符串。  
    ```
    var stringValue = "hello world";
    
    console.log(stringValue.slice(3));          //"lo world"
    console.log(stringValue.substring(3)));     //"lo world"
    console.log(stringValue.substr(3));         //"lo world"
    
    console.log(stringValue.slice(3, 7));       //"lo w"
    console.log(stringValue.substring(3, 7));   //"lo w"
    console.log(stringValue.substr(3, 7));      //"lo worl"
    ```  