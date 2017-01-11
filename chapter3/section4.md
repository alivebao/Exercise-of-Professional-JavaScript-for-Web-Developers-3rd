# 第四节 操作符和语句
1. ==和!=的作用是？  
  答："=="代表相等，先转换再比较。  
  转换不同数据类型时，==和!=的规则为:  
  1. 如果有一个操作数是布尔值，在比较相等前先将其转换为数值(false->0, true->1)。
  2. 如果有一个操作数是字符串，另一个操作数是数值，在比较相等性前先将字符串转换为数值。
  3. 如果一个操作数是对象，另一个不是，则调用对象的valueOf方法，用得到的基本类型值按之前规则进行比较。
  ==和!=在进行比较时需要遵守的规则：
  1. null和undefined是相等的。
  2. 若有一个操作数是NaN，相等操作符返回false，不等操作符返回true。
  3. 若两个操作数都是对象，比较它们是否指向同一个对象。
  
2. ===和!==的作用是？和==/!=的区别在于？  
  答："==="代表全等，和==/!=相比，除了在比较前不转换外，其他地方没什么区别。
  
3. 逗号操作符的作用是？  
  答：使用逗号操作符可以在一条语句中执行多个操作，用于声明多个变量，返回表达式中的最后一项。
  ```
  var num = (1, 2, 5, 8); //num的值为8
  ```
4. for-in语句的作用是？  
  答：for-in是一种精准的迭代语句，可用来每句对象的属性，用法为：
  ```
  //for(property in expression) statement
  for (var propName in window) {
    document.write(propName)
  }
  ```
  如果表示要迭代的对象的变量值为__null或undefined__，for-in语句会抛出错误。ES5更正了这一行为(对这种情况不再抛出错误，而只是不执行循环体)。为保证最大程度的兼容性，建议在使用for-in循环前，先检测确认该对象是否为null/undefined。  
  
5. with语句的作用是？
  答：with语句将代码的作用域设置到一个特定的对象中，主要是为了简化多次编写同一个对象的工作。  
  如：
  ```
  var qs = location.search.substring(1);
  var hostName = location.hostName;
  var url = location.href;
  ```  
  可以简写为：
  ```
  with(location){
    var qs = search.substring(1);
    var hostName = hostName;
    var url = href;
  }
  ```
  