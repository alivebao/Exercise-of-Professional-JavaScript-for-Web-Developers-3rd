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
  这里t能够访问到returnAFunction中的param1和pre，是因为returnAFunction内部函数的作用域链中包含returnAFunction的作用域。  
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
  createFunctions会返回一个函数数组，该数组中各函数的功能是返回i，他们的作用域链均保存着createFunctions的活动对象。  
  也就是说，这些函数在调用i时实际上引用的都是createFunctions中的i。当createFunctions执行完后，i的值是10，因此这些函数的返回值都是10。  
  作用域链关系如图所示：  
  ![作用域链](../../res/pic/7_1_2.jpg)  
  可以通过创建另一个匿名函数强制让闭包的行为符合预期:  
    ```
    function createFunctions(){
        var result = new Array();
        
        for(var i = 0 ; i < 10 ; i++){
            result[i] = function(num){
                return function(){
                    return num;
                };
            }(i);
        }
        
        return result;
    }
    var result = createFunctions();
    result[1]();        //1
    result[9]();        //9
    ```  
  这里result保存的是各函数的执行结果，可以这么理解：  
    ```
    function createFunctions(){
        var result = new Array();
        
        var anoFunction = function(param){
            var getOuterParam = function(){
                return param;
            }
            return getOuterParam;
        }
        
        for(var i = 0 ; i < 10 ; i++){
            
            result[i] = anoFunction(i);
        }
        
        return result;
    }
    var result = createFunctions();
    result[1]();        //1
    result[9]();        //9
    ```  
  如图所示，anoFunction返回了一个函数getOuterParam，该函数的功能为返回anoFunction调用时的参数param。  
  执行anoFunction(i)的返回值为参数i。  
  ![作用域链](../../res/pic/7_1_3.jpg)  
    
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
  obj.getNameFunc返回了一个匿名函数，这个函数的函数体为return this.name。  
  在全局环境下调用该函数时，该函数的this会被设为window。  
  由于该函数有this参数，因此不会访问obj中的this，打印结果为The Window。如图所示。  
  ![作用域链](../../res/pic/7_1_4.jpg)  
  可以通过以下操作让闭包访问对象属性：  
    ```
    var name = "The Window";
    
    var obj = {
        name: "My Obj",
        getNameFunc: function() {
            var that = this;
            return function() {
                return that.name;
            }
        }
    }
    
    console.log(obj.getNameFunc()());   //My Obj
    ```  
  调用该函数时，该匿名函数返回that.name。  
  由于该匿名函数中没有that参数，会通过作用域链访问外部函数getNameFunc的that，也就是obj的this，因此打印结果为My Obj。  
  ![作用域链](../../res/pic/7_1_5.jpg)  
  
