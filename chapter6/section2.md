# 第二节 创建对象-工厂模式和构造函数模式
1. 什么是工厂模式？使用工厂模式创建一个对象。  
    答：工程模式抽象了创建具体对象的过程，用函数封装以特定接口创建对象的细节。  
    ```
    function createPerson(name, age){
        var o = new Object();
        o.name = name;
        o.age = age;
        o.sayName = function() {
            console.log(o.name);
        }
        return o;
    }
    
    var person1 = createPerson("John", 29);
    var person2 = createPerson("Jack", 24);
    ```  
    __工厂对象虽然解决了创建多个相似对象的问题，但却没有解决对象识别的问题(即怎样知道一个对象的类型)。__
2. 什么是构造函数模式？用构造函数模式创建一个对象。  
    ```
    function Person(name, age){
        this.name = name;
        this.age = gae;
        this.sayName = function() {
            console.log(this.name);
        }
    }
    
    var person1 = new Person("John", 29);
    var person2 = new Person("Jack", 24);
    ```  
3. 构造函数与工厂模式的区别？      
    1. 在Person函数中，没有显式的创建对象。  
    2. 直接将属性和方法赋给了this对象。  
    3. 没有return语句。    
4. var person1 = new Person("John", 29)这一过程中，new的作用是？      
  答：要创建Person的新实例，必须使用__new__操作符。  
  采用该方式调用构造函数会经历以下4个步骤：  
    1. 创建一个新对象。  
    2. 将构造函数的作用域赋给新对象(因此this就指向了这个新对象)。  
    3. 执行构造函数中的代码(为这个新对象添加属性)。  
    4. 返回新对象。  
   
5. 如何检测对象person1和person2的类型？  
  答：可以通过instanceOf操作法检测对象的类型：  
    ```
    console.log(person1 instanceof Object); //true
    console.log(person1 instanceof Person); //true
    console.log(person2 instanceof Object); //true
    console.log(person2 instanceof Person); //true
    ```    
6. 构造函数和普通函数的区别？  
  答：构造函数也是函数，其与其他函数的唯一区别在于调用方式不同。  
  任何函数，只要通过new操作符来调用，就可以作为构造函数。  
  任何函数，如果不通过new操作符来调用，就是普通函数。  
  在上面的例子中，将Person作为普通函数进行调用：
    ```
    //构造函数
    var person = new Perons("Nic", 25);
    person.sayName();   //Nic
    //普通函数
    Person("Gerg", 30);
    window.sayName();   //Grey
    //在另一个对象的作用域中调用
    var o = new Object();
    Person.call(o, "Des", 27);
    o.sayName();        //Des
    ```  
7. 构造函数存在什么缺点？  
  答：在之前的例子中，person1和person2都有一个名为sayName的方法，这两个方法__不是同一个Function的实例__：  
    ```
    console.log(person1.sayName == person2.sayName);     //false
    ```  
  为解决__两个方法不是同一个Function实例的问题，__可以通过该方式处理：  
    ```
    function Pesron(name, age) {
        this.name = name;
        this.age = age;
        this.sayName = sayName;
    }
    //将sayName定义为全局函数，作为引用传递给Person的this.sayName： 
    function sayName() {
        console.log(sayName);
    }
    var person1 = new Person("Nic", 27);
    var person2 = new Person("Jessy", 25);
    ```  
  但采用这种方式，sayName似乎是Person的专属函数，作为全局函数不太合适。  
  而且，若对象需要定义许多方法，就要定义多个全局函数，这将导致这个自定义的类__毫无封装性可言__。
  