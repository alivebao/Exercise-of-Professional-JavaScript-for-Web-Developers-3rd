# 第四节 创建对象-动态原型模式和寄生构造函数模式
1. 介绍一下动态原型模式？  
  答：动态原型模式将类的.prototype的赋值移入了构造函数中，通过判断其中的方法类型是否为"function"完成对prototype相应参数的初始化。  
    ```
    function Person(name, age){
        this.name = name;
        this.age = age;
        
        if(typeof this.sayName != "function"){
            Person.prototype.sayName = function() {
                console.log(this.name);
            }
        }
    }
    ```  
2. 介绍一下寄生构造模式？  
  答：除了创建对象时采用new的方法，该模式与工厂模式的写法完全一样。  
    ```
    function Person(name, age){
        var o = new Object();
        o.name = name;
        o.age = age;
        o.sayName = function() {
            console.log(this.name);
        }
        return o;
    }
    var person = new Person("Nic", 27);
    person.sayName();
    ```  
  当我们想对现有的某个类进行属性增强时，出于安全考虑不应该直接修改该类的prototype，可以考虑采用这种方式：  
    ```
    function SpecialArray() {
        var values = new Array();
        values.push.apply(values, arguments);
        values.toPipedString = function() {
            return this.join("|");
        };
        
        return values;
    }
    var colors = new SpecialArray("red", "blue", "green");
    console.log(colors.toPipedString());    //"red|blue|green"
    ```  
    注意，这种方式创建的对象无法依赖instanceof操作法确定对象类型。可以使用其他模式的情况下尽量不要使用这种模式。  