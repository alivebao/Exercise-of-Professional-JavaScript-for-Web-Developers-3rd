# 第六节 继承-原型式继承、寄生式继承和寄生组合式继承
1. 什么是原型式继承？其使用场景是？  
  答：借助原型可以基于已有的对象创建新对象，同时还不必因此创建自定义类型：  
    ```
    function object(o){
        function F(){}
        F.prototype = o;
        return new F();
    }
    ```  
  在object函数内部创建一个临时性的构造函数，将传入的对象作为其原型，返回该类型的新实例。本质上object()对传入的对象执行了一次浅复制。  
  也就是ES5中的Object.create(instance[, params])，其参数为用作新对象的原型对象和(可选的)一个为新对象定义额外属性的对象：  
    ```
    var person = {
        name: "Nic",
        friends: ["A", "B"]
    };
    
    var anotherPerson = Object.create(person, {
        name: {
            value: "Jack"
        }
    });
    
    console.log(anotherPerson.name);    //"Jack"
    
    person.friends.push("C");
    console.log(anotherPerson.friends); //"C"
    ```  
  适用于在没有必要创建构造函数，只是想__让一个对象与另一个对象保持类似__的情况下。  
2. 什么是寄生式继承？其使用场景是？  
  答：类似于寄生构造函数+工厂模式。  
    ```
    function createAnother(original){
        var clone = Object.create(original);
        clone.sayHi = function() {
            console.log("hi");
        };
        return clone;
    }
    
    var person = {
        name: "Nic"
    };
    
    var anotherPerson = createAnother(person);
    anotherPerson.sayHi();      //"Nic"
    ```    
  在主要考虑对象而不是自定义类型和构造函数的情况下，寄生式继承也是一种有用的模式。  
  使用寄生式继承未对象添加函数会由于不能做到函数复用而降低效率，这一点类似与构造函数模式。  
3. 什么是寄生组合式继承？相较与组合继承，其优点是？  
  答：组合继承最大的问题在于总会调用两次超类构造函数:  
    ```
    function SuperType(name){
        this.name = name;
    }
    SuperType.prototype.sayName = function(){
        console.log(name);
    }
    
    function SubType(name, age){
        SuperType.call(this, name);             //第二次调用SuperType()
        this.age = age;
    }
    SubType.prototype = new SuperType();        //第一次调用SuperType()
    SubType.prototype.constructor = SubType;
    SubType.prototype.sayAge = function(){
        console.log(this.age);
    }
    ```  
  寄生组合式继承__通过借用构造函数来继承属性，通过原型链的原型式继承形式来继承方法__。  
  寄生组合式继承至调用了一次SuperType构造函数，并因此避免了在SubType.prototype上创建不必要的、多余的属性：  
    ```
    function inheritPrototype(subType, superType){
        var prototype = object(superType.prototype);
        prototype.constructor = subType;
        subType.prototype = prototype;
    }
    
    function SuperType(name){
        this.name = name;
    }
    SuperType.prototype.sayName = function(){
        console.log(name);
    }
    
    function SubType(name, age){
        SuperType.call(this, name);             //第二次调用SuperType()
        this.age = age;
    }
    
    inheritPrototype(subType, superType);
    
    SubType.prototype.sayAge = function(){
        console.log(this.age);
    }
    ```  
  寄生组合式继承是引用类型最理想的继承方式。  