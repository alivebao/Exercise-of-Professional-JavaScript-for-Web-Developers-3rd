# 第五节 函数
1. 谈谈对函数中参数的理解？  
  答：ECMAScript函数的参数与大多其他语言中函数的参数不同。  
  1. 其不在乎传递进来的参数个数。
  2. 其不在乎传递进来的参数类型。  
  在ECAMScript中，其向函数传递的实际上是一个arguments对象，该对象与数组类似(__仅仅是类似，并不是Array的实例__)，可以使用方括号语法访问其每一个元素。如：
  ```
  function printFunctionParamLength(){
    console.log(arguments.length);  //print the num of param in this function
  }
  ```  
  
  未传递值的命名参数将自动被赋予undefined值：
  ```
  function printParam2(param1, param2){
    console.log(param2);
  }
  printParam2(1); //undefined
  ```
  
2. ECMAScript的函数中是否有重载？  
  答：没有。在ECMAScript中定义两个名字相同的函数，则该名字只属于后定义的函数。
  ```
  function funTest(param1, param2) {
    console.log("funTest2")
  }
  
  function funTest(param1) {
    console.log("funTest1");
  }
  
  funTest(1, 2); //funTest1
  ```
  如1所述，ECMAScript中的参数个数并不能代表什么，其实际上是一个arguments对象，因此，funTest(param1)实际上是将函数funTest重新覆盖了一遍。