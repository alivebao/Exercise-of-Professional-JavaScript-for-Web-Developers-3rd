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