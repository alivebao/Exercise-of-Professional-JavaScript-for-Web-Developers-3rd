# 第三节 数据类型2-Number/String/Object
  1. 什么是Number类型？  
   答：Number最基本的数值字面量格式是十进制整数，此外还有八进制(以0开头，__在严苛模式下无效，会导致支持该模式的JS引擎抛出错误__)、十六进制等(以0x开头)。  
   浮点数是指包含小数点且小数点后面必须至少有一位数字的数。保存浮点数需要的内存空间是整数的两倍，ECMAScript会不失时机的将其转换为整数。如小数点后面未跟任何数字(如1.)/浮点数本身就是一个整数(如1.0)等情况。  
   需要注意的是浮点数的计算。其精度在计算时非常糟糕：  
   ```
   var a = 0.1 , b = 0.2;
   console.log(a + b === 0.3) // false
   ```
   a + b 返回的值是0.30000000000000004。当需要判断两个浮点数是否相等时，可以采用以下方式：  
   ```
   var a = 0.1 , b = 0.2;
   console.log(a + b - 0.3 < 0.0000001) // true
   ```     
   数值超过Number可表示的范围时，会得到Infinity/-Infinity的值。  
   NaN：Not a Number。任何数值除以非数值均会返回NaN，其有两个特点：  
   1. 任何涉及NaN的操作均会返回NaN。  
   2. NaN与包括其本身在内的任何值都不相等，通过isNaN(param)判断参数param是否为NaN。  
   
  2. 数值转换，Number()/parseInt()/parseFloat()的区别？  
    3个可以把非数字转换为数值的函数：Number()/parseInt()/parseFloat()  
    Number()的转换规则：  
      1. Boolean: true->1, false->0  
      2. Number: 不做操作  
      3. null: 0
      4. undefined: NaN
      5. String:  
        1. 字符串只包含数字(包括带正负号的情况)：转为十进制数字
        2. 字符串包含有效浮点格式：转为相应浮点数值
        3. 包含有效十六进制：转为大小相同的十进制
        4. 包含有效八进制：忽略前导0，直接转为十进制
        5. 空字符串：0
        6. 其他：NaN
      6. object: 调用对象的valueOf(),然后依照上面的规则转换返回的值。  
   
    parseInt()的转换规则：在转换字符串时，更多的是看起是否符合数值模式
      1. 忽略字符串前面的空格直到第一个非空格字符。若该字符不是数字字符或符号，负号，返回NaN
      2. 若第一个字符是数字字符，则会继续解析第二个字符直到解析完所有后续字符或遇到一个非数字字符
      ```
      parseInt("123va12");  //123
      parseInt("");         //NaN
      parseInt("0xA");      //10
      parseInt("22.5");     //22
      ```
      解析八进制时，ECMAScript3和ECMAScript5存在区别：
      ```
      parseInt("070")       //ECMAScript3-56(八进制), ECMAScript5-70(十进制)
      ```
      可以通过为parseInt设置第二个参数定义转换时使用的基数：
      ```
      parseInt("AF")        //NaN
      parseInt("AF", 16)    //175
      parseInt("10", 8)     //8
      ```
    parseFloat类似parseInt, 区别在于其支持浮点数且不支持基数设置(没有第二个参数)。  
  3. 字符串的值能否改变？  
    答：字符串一旦创建，其值就不能改变。
    ```
    var text = "hello"
    text = text + "world";
    ```   
    执行过程为：首先在内存(假设内存地址为a)中创建字符串"hello",在text中保存其地址a。然后创建新的字符串"world"(假设地址为b),将"hello"与"world"拼接成一个新的字符串(假设地址为c)，text中保存c的值。  
  4. 在不确定要转换的值是否为null/undefined时，如何将其转换为String类型？  
    答：一般使用toString函数将值转换为String类型。但当要转换的值为null/undefined时，执行toString()会产生错误。这时可以使用转型函数String()。
    ```
    var a = 10;
    var b = true;
    var c = null;
    var d;
    console.log(String(a)); //"10"
    console.log(String(b)); //"true"
    console.log(String(c)); //"null"
    console.log(String(d)); //"undefined"
    ```
  5. 每个Object实例都具有的属性和方法是？  
    答：
      1. constructor: 保存用于创建当前对象的函数
      2. hasOwnProperty(propertyName): 用于检测给定属性在当前实例中是否存在
      3. isPrototypeOf(Object): 用于检测传入的对象是否是当前对象的原型
      4. propertyIsEnumerable(propertyName): 用于检测给定属性是否能够使用for-in语句进行枚举
      5. toLocaleString(): 返回对象的字符串表示，该字符串与执行环境的地区对应
      6. toString(): 返回对象的字符串表示
      7. valueOf(): 返回对象的字符串、数值或布尔值表示，通常与toString()方法的返回值相同