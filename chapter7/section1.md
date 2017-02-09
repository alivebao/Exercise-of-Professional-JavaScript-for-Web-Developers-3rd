# 第一节 闭包
1. 匿名函数与闭包的区别以及闭包的实现原理？  
  答：匿名函数-没有名称的函数。  
  闭包-一个有权访问另一个函数作用域中的变量的函数。  
    ```
    function returnAFunction(param1){
        var pre = param1 + " ";
        return function(name){
            console.log(pre + name);
        };
    }
    
    var t = returnAFunction("HELLO");
    t("MIKE");    //Hello Mike
    ```  
  这里t能够访问到returnAFunction中的param1/pre，是因为returnAFunction内部函数的作用域链中包含returnAFunction的作用域。  
  当某个函数被调用时，会创建一个执行环境及相应的作用域链，并使用arguments和其他命名参数初始化函数的活动对象。  
  此外，作用域链中还包含__外部函数的活动对象(处于作用域链中的第二位)__、__外部函数的外部函数的活动对象(作用域链中的第三位)...__  
  上例作用域链如图所示：  
  ![作用域链](../../res/pic/7_1_1.jpg)  
  正常情况下returnAFunction执行完后其活动对象应被销毁，但这里由于存在闭包，returnAFunction的活动对象被添加至匿名函数的作用域链中，因此这些活动对象仍会被保留。直到他们不再存在于任何作用域链(匿名函数被销毁)后这些活动对象才会被销毁。  
    ```
    //匿名函数被销毁，其作用域链随之销毁
    //returnAFunction()的活动对象不再存在于任何作用域链中，被销毁
    t = null;   
    ```  