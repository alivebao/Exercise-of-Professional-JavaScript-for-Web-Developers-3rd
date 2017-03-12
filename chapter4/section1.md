# 第一节 基本类型和引用类型的值  
1. JS的5种基本类型是？  
  答：Undefined, Null, Boolean, Number和String.很多语言中的String为引用类型，在JS中，String为基本类型(__注意和其他语言的区别__)。  
  
2. 什么是引用类型，和基本类型的区别是什么？  
  答：JS可能包含两种不同数据类型的值(基本类型和引用类型)。  
  __基本类型值__指的是简单的数据段，按值访问的，变量中存放的是基本类型的实际值。  
  __引用类型值__指的是可能由多个值构成的对象，按引用访问的，变量中存放的是对象的引用(JS不允许直接访问内存中的位置，也就是说不能直接操作对象的内存空间。在操作对象时实际是在操作对象的引用而非实际对象。引用和指针都是地址的概念，但引用是一个存储对象的别名，指针指向一个内存对象，保存着该对象的内存地址。)  
  
  1. 引用类型可以动态的添加属性，基本类型则不行。    
    ```
    var person = {};
    person.name = "Hello";
    console.log(person.name); //Hello
  
    var name = "World";
    name.age = 24;
    console.log(name.age); //undefined
    ```
  2. 复制变量的方式不同。  
  如图所示，  
  ![JavaScript组成部分](../../res/pic/4_1.jpg)  
  基本类型变量间用"="赋值时直接将值进行复制，赋值完成后新变量中存放的值与原变量中的值相互独立。引用类型变量间用"="赋值时传递的是变量的引用，赋值完成后新变量中存放的值与原变量中的值均为对某对象的引用，两者指向同一对象。    
    ```
    var num1 = 5;
    var num2 = num1;
    num2 = 10;
    console.log(num1);    //5
    console.log(num2);    //10
  
    var obj1 = {};
    obj1.name = "Hello";
    var obj2 = obj1;
    obj2.name = "World";
    console.log(obj1.name);//World
    console.log(obj2.name);//World
    ```  
    可以看到，将num1(基本类型)中的值赋值给num2后，修改num2中的值并不影响num1.将obj1(引用类型)中的值赋值给obj2轴，修改obj2的name属性为"world"，由于obj1和obj2__引用着内存空间中的同一对象__，因此console.log(obj1.name)的结果同样为"World"。  
  
3. 向函数传参的过程中，对于引用类型是按值传递还是按引用传递？如何证明？   
  答：按值传递。__ECMAScript中所有函数的参数都是按值传递的__。在向参数传递基本类型的值时，被传递的值会被复制给一个局部变量。传递引用类型时，会把这个值在内存中的地址复制给一个局部变量。__因此，这个局部变量的变化会反应在外部，会影响到原引用类型__  
  ```
  function setName(obj){
    obj.name = "Hello";
    obj = new Object();
    obj.name = "World";
  }
  
  var person = new Object();
  setName(person);
  console.log(person.name); //Hello
  ```
  由于是按值传递，setName中第一行obj.name = "Hello"会影响到原引用类型，此时person.name的值为Hello。  
  在第二行中给obj重新new了一个object，此时obj指向了一个新的对象。  
  若是按引用传递，则person也将指向同一个新对象。将新对象的name设为World，person.name同样应收到影响。
  若是按值传递，则仅是函数内的obj指向新对象，person在此之后与obj不在关联，对obj.name的赋值不会影响person。  
  打印结果证明函数是按值传递的。
  
4. typeof是用于检测String/Number/Boolean/Undefined的有效工具，但对null或对象，typeof均会返回"object"。应如何确定某对象是什么类型的？  
  答：使用instanceof操作符。若变量是给定引用类型的实例，则instanceof操作法就返回true
  ```
  var colors = ["red", "green"];
  console.log(colors instanceof Array); //true
  ```
  根据规定，所有引用类型的值都是Object的实例，因此在检测一个引用类型值和Object构造函数时，instanceof始终返回true。  
  __如果使用instanceof操作符检测基本类型的值，该操作法始终返回false，因为基本类型不是对象。__