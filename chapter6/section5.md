# 第五节 继承-原型链、借用构造函数和组合继承
1. 以下为实现原型链继承的基本模式，请画出该例中实例、构造函数及原型间的关系图(不需要画出Object Prototype)。  
    ```
    function SuperType(){
        this.property = true;
    }
    SuperType.property.getSuperValue = function(){
        return this.property;
    };
    
    function SubType(){
        this.subproperty = false;
    }
    SubType.prototype = new SuperType();
    SubType.prototype.getSubValue = function(){
        return this.subproperty;
    };
    
    var instance = new SubType();
    console.log(instance.getSuperValue);    //true
    ```  
    
  答：关系图如图所示。需要注意的地方是：  
  由于执行了```SubType.prototype = new SuperType()```，这时SubType.prototype实际上成为了SuperType()的一个实例。  
  因此，在SubType的prototype中会有指向SuperType Prototype的[[Prototype]]以及SuperType的属性property。  
  ![实例、构造函数、原型关系图1](../../res/pic/6_5_1.jpg)  
  
2. 原型链继承中存在哪些问题？  
  答：
  1. 在SuperType构造函数中定义的引用类型的属性(如this.arrNames=["A", "B", "C"])，会被SubType中的所有instance共享：  
    ```
    function SuperType(){
        this.arrNames = ["A", "B", "C"];
    }
    function SubType(){
    }
    SubType.property = new SuperType();
    
    var instance1 = new SubType();
    instance1.arrNames.push("D");
    console.log(instance1.arrNames);    //"A", "B", "C", "D"
    
    var instance2 = new SubType();
    console.log(instance2.arrNames);    //"A", "B", "C", "D"
    ```  
  原因如图所示，可以看到SubType中的arrNames实际上是SubType Prototype中的属性，instance1和instance2访问的实际上是同一个arrNames：  
  ![实例、构造函数、原型关系图2](../../res/pic/6_5_2.jpg)  
  2. 创建子类实例时，无法向超类型的构造函数中传递参数。  
  
3. 简述借用构造函数的思路？  
  答：在子类的构造函数中通过apply()/call()调用超类的构造函数，相当于让超类在子类中重新执行一次，使得子类具有超类的属性/方法。  
    ```
    function SuperType(){
        this.arrNames = ["A", "B", "C"];
    }
    function SubType(){
        SuperType.call(this);
    }
    
    var instance1 = new SubType();
    instance1.arrNames.push("D");
    console.log(instance1.arrNames);    //"A", "B", "C", "D"
    
    var instance2 = new SubType();
    console.log(instance2.arrNames);    //"A", "B", "C" 
    ```  
  这样做的好处在于解决了原型链中的两个问题(见问题2)。  
  但是，这种方式存在一个问题，__由于方法都定义在构造函数中，因此无法进行函数复用__。  
  为此，可以采用组合继承的方式，组合原型链和借用构造函数的思路达到较好的继承效果。  

4. 简述组合继承？  
  答：组合继承避免了原型链和借用构造函数的缺陷，融合了两者的优点，成为了__JavaScript中最常用的继承模式__。
    ```
    function SuperType(name){
        this.name = name;
        this.colors = ["r", "g"];
    }
    SuperType.property.sayName = function(){
        console.log(this.name);
    };
    
    function SubType(name, age){
        SuperType.call(this, name);
        this.age = age;
    }
    SubType.prototype = new SuperType();
    SubType.prototype.constructor = SubType;
    SubType.prototype.sayAge = function() {
        console.log(this.age);
    }
    
    var instasnce1 = new SubType("Nic", 21);
    instance1.colors.push("B");
    console.log(instance1.colors);  //"r", "g", "b"
    instance1.sayName();            //"Nic"
    instance1.sayAge();             //21
    
    var instasnce1 = new SubType("Ali", 24);
    console.log(instance2.colors);  //"r", "g"
    instance2.sayName();            //"Ali"
    instance2.sayAge();             //24
    ```  
