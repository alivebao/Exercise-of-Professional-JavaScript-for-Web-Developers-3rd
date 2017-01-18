# 第三节 Function类型
1. 函数是对象吗？函数名实际上是什么？  
  答：函数是Function类型的实例，是对象。函数名实际上是指向一个函数对象的指针。用这种方法写更加容易理解(实际应用中不推荐，只是为了便于理解)：```var sum = new Function("num1", "num2", "return num1 + num2")```  
  
2. 函数声明与函数表达式的区别？  
  答：解析器在向执行环境中加载数据时，会率先读取函数声明，使其在执行任何代码前可用(可访问)。
  对于函数表达式，则必须等待解析器执行到其所在代码行时才会真正被解释执行：  
    ```
    console.log(sum1(1, 2));    //3
    console.log(sum2(1, 2));    //sum2 is not defined
    function sum1(num1, num2) {
        return num1 + num2;
    }
    var sum2 = function(num1, num2) {
        return num1 + num2;
    };
    ```  
  除了什么时候可以通过变量访问函数这一点区别外，函数声明和函数表达式的语法其实是等价的。  
  
3. 介绍一下函数中的callee和caller？  
  答：callee是一个指针，指向拥有这个arguments对象的函数。  
    ```
    function factorial(num){
        if(num <= 1){
            return 1;
        }else {
            return num * arguments.callee(num - 1);
        }
    }
    ```  
  caller保存着调用当前函数的函数的引用，若在全局作用域中调用当前函数，则该值为null。  
    ```
    function outer(){
        inner();
    }
    function inner(){
        console.log(inner.caller);
    }
    outer();    //'function outer(){inner()}';
    ```  
  函数在严苛模式下运行时执行arguments.callee/caller会导致错误。    为区分__arguments.caller__和函数的__caller__属性，ES5定义了arguments.caller属性。严苛模式下访问该属性会导致错误，非严苛模式下该属性始终为undefined.  
  
4. 函数的length属性有何作用？  
  答：length用于表示函数希望接收的命名参数的个数。  
    ```
    function printHello() {
        console.log('hello');
    }
    function printName(name) {
        console.log(name);
    }
    function printSum(num1, num2) {
        console.log(num1 + num2);
    }
    console.log(printHello.length); // 0
    console.log(printName.length);  // 1
    console.log(printSum.length);   // 2
    ```  
    
5. 函数的apply()和call()方法有什么作用？  
  答：两个函数均用于设置函数的this对象，区别仅在于接收参数的方式不同。  
  apply()接受两个参数-运行函数的作用域和参数数组。  
  call()中第一个参数是this值，其余参数都直接传递给函数，即使用该方法时，传递给函数的参数必须逐个列举出来。  
    ```
    function sum(num1, num2){
        return num1 + num2
    }
    function callSumbyApply(num1, num2){
        return sum.apply(this, [num1, num2]);
    }
    function callSumbyCall(num1, num2){
        return sum.call(this, num1, num2);
    }
    ```  
  这两个函数的主要用途在于设置函数的作用域：  
    ```
    window.color = "red";
    var o = {color: "blue"};
    
    function printColor() {
        console.log(this.color);
    }
    
    printColor();               //red
    printColor.call(this);      //red
    printColor.call(window);    //red
    printColor.call(o);         //blue
    ```    

6. 介绍以下bind函数？  
  答：该方法会创建一个函数的实例，其this值会被绑定到传给bind()函数的值。  
    ```
    window.color = "red";
    var o = {color: "blue"};
    
    function printColor() {
        console.log(this.color);
    }
    
    var objectPrintColor = printColor.bind(o);
    objectPrintColor();         //blue
    ```  
  这里printColor()调用bind并传入了对象o，创建了objectPrintColor函数，该函数的this值被设置为等于o，即使在全局作用域中调用该函数，其打印的值也仍为o中的color。