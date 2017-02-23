# 第七章 函数表达式

## 第一节 闭包
  1. 匿名函数与闭包的区别以及闭包的实现原理？  
  2. 以下代码的返回值是？  
    ```
    function createFunctions(){
        var result = new Array();
        
        for(var i = 0 ; i < 10 ; i++){
            result[i] = function(){
                return i;
            };
        }
        return result;
    }
    var result = createFunctions();
    result[1]();      //10;
    result[9]();      //10;
    ```  
  3. 以下代码的返回值是？  
    ```
    var name = "The Window";
    
    var obj = {
        name: "My Obj",
        getNameFunc: function() {
            return function() {
                return this.name;
            }
        }
    }
    
    console.log(obj.getNameFunc()());   //The Window
    ```  
    
# 第二节 块级作用域和私有变量
  1. 如何实现块级作用域？  
  2. 什么是__私有变量__？  
  3. 什么是__特权方法__？如何创建特权方法？    
  4. 分析比较以下两种访问私有变量的方式:
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