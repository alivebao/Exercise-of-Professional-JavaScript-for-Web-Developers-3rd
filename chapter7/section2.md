# 第二节 块级作用域和私有变量
1. 如何实现块级作用域？  
  可以通过匿名函数实现。在ES6中，可以通过关键字let实现。  
    ```
    //通过匿名函数实现
    (function() {
        var i = 1;
    })();
    {
        let j = 2;
    }
    
    console.log(i); //Uncaught ReferenceError
    console.log(j); //Uncaught ReferenceError
    ```

2. 什么是__私有变量__？  
  任何在函数中定义的变量，都可以认为是私有变量。因为不能在函数的外部访问这些变量。  
  私有变量包括函数的参数、局部变量和在函数内部定义的其他函数(又被称为私有函数)。  
  
3. 什么是__特权方法__？如何创建特权方法？    
  特权方法是__有权访问私有变量和私有函数的公有方法__。  
  可以在构造函数中定义特权方法：  
    ```
    function MyObj(){
        //私有变量
        var privateVariable = 10;
        //私有函数
        function privateFunction(){
            return privateVariable;
        }
        
        //特权方法
        this.publicMethod = function(){
            privateVariable++;
            return privateFunction();
        };
    }
    
    var a = new MyObj();
    console.log(a.privateVariable);     //undefined
    console.log(a.privateFunction());   //Uncaught TypeError
    console.log(a.publicMethod());      //11
    ```  
  这里只能通过a.publicMethod()访问a的私有变量。  
  
4. 分析比较以下两种访问私有变量的方式：
    ```
    //方式1
    (function(){
        var privateVariable = 10;
        
        function privateFunction(){
            return privateVariable;
        }
        
        MyObj1 = function(){        
        }
        
        MyObj1.prototype.publicMethod = function(){
            privateVariable++;
            return privateFunction();
        };
    })()
    
    var obj1 = new MyObj1();
    console.log(obj1.publicMethod());   //11
    //方式2
    function MyObj2(){
        //私有变量
        var privateVariable = 10;
        //私有函数
        function privateFunction(){
            return privateVariable;
        }
        
        //特权方法
        this.publicMethod = function(){
            privateVariable++;
            return privateFunction();
        };
    }
    var obj2 = new MyObj2();
    console.log(obj2.publicMethod());   //11
    ```  
  方式1在严格模式下会出错。  
  其通过```MyObj1 = function(){}```，由于未在其之前加var，使得MyObj1成为全局变量。  
  这种方式访问的是静态私有变量，所有通过new MyObj1()创建出的实例，均共享同一个privateVariable和privateFunction。  
      
  方式2采用的是构造函数的方式进行创建的，没有共享私有变量，每个实例均有独自的私有变量。  
