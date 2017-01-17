# 第二节 RegExp类型
1. 以字面量形式创建一个正则表达式的方法是？  
  答：var expression = / pattern / flags;  
  其中pattern部分可以是任何简单或复杂的正则表达式，flags为该表达式的标识。  
  
2. 介绍一下正则表达式的匹配模式支持的3个标志(g/i/m)？  
  1. g: 全局模式，模式将被应用与所有字符串，而非在发现第一个匹配项时立即停止；  
  2. i：不区分大小写模式，在确定匹配项时忽略模式与字符串的大小写；  
  3. m：多行模式，在到达一行文本莫问时还会继续查找下一行中是否存在与模式匹配的项。  
  
3. 正则表达式的模式中使用的所有__元字符__都必须转义，正则表达式中的元字符有哪些？  
  答：( [ { \ ^ $ | ) ? * + . ] }

4. 用RegExp的构造函数构建一个与```var pattern1 = /\[bc\]at/i```等价的表达式？  
  答：```var pattern2 = new RegExp("\\[bc\\]at", "i");```  
  这里需要注意的是，由于RegExp构造函数的模式参数是字符串，所以某些情况下要对字符进行__双重转义__。  
  __所有的元字符__都必须双重转义，那些已经转义过的字符也是如此。  
  
5. 使用正则表达式字面量和使用RegExp构造函数创建的正则表达式的区别？  
  答：ES3中，正则表达式字面量始终会共享同一个RegExp实例，使用构造函数创建的每一个新RegExp实例都是一个新实例。  
  ES5中则已经无区别了，其明确规定使用正则表达式字面量必须向直接调用RegExp构造函数一样，每次都创建新的RegExp实例。  
  
6. 介绍一下RegExp的实例属性？  
  答：
  1. global：布尔值，表示是否设置了g标志。  
  2. ignoreCase：布尔值，表示是否设置了i标志。  
  3. multiline：布尔值，表示是否设置了m标志。  
  4. lastIndex：整数，表示开始搜索下一个匹配性的字符串位置，从0算起。  
  5. source：正则表达式的字符串表示，按照__字面量形式__而非传入构造函数中的字符串模式返回。  
  
7. 介绍一下RegExp的实例方法？  
  答：
  1. exec：RegExp对象的主要方法，专门为捕获组而设计。  
  exec()接受一个参数，即要应用模式的字符串，然后返回包含第一个匹配项信息的数字；或在没有匹配项的情况下返回null。返回的数组虽然是Array的实例，但包含index和input两个额外属性。  
    1. index：表示匹配项在字符串中的位置。  
    2. input：表示应用正则表达式的字符串。  
  例：  
  
    ```
    var text = "mom and dad and baby";
    var pattern = "/mom( and dad( and baby)?)?/gi;
  
    var matches = pattern.exec(text);
    console.log(matches.index);   //0
    console.log(matches.input);   //"mom and dad and baby"
    console.log(matches[0]);      //"mom and dad and baby"
    console.log(matches[1]);      //" and dad and baby"
    console.log(matches[2]);      //" and baby"
    ```  
  对于exec()而言，计算在模式中设置了全局标志(g)，其每次也只会返回一个匹配项。  
  在不设置全局变量的情况下，在同一个字符串上多次调用exec()将始终返回第一个匹配项的信息。  
  在设置全局变量的情况下，每次调用exec()都会在字符串中继续查找新匹配项。  
  
  2. test(): 接受一个字符串参数。在模式与该参数匹配的情况下返回true，否则返回false。  
  3. toString/toLocalString：返回正则表达式的字面量，与创建正则表达式的方式无关。
  
