# 第三节 创建对象-原型模式
1. 什么是prototype属性？简单介绍一下函数的prototype属性。  
  我们所创建的每个函数都有一个prototype属性，该属性是一个指针，指向一个__原型对象__，该函数的所有实例都可以通过prototype共享其属性和方法：  
    ```
    function Person(){
    }
    Person.prototype.name = "Nic";
    Person.prototype.age = 29;
    Person.prototype.sayName = function() {
        console.log(this.name);
    }
    
    var person1 = new Person();
    person1.sayName();  //Nic
    
    var person2 = new Person();
    person2.sayName();  //Nic
    
    console.log(person1.sayName == person2.sayName);    //true
    ```  

2. 什么是原型对象，其包含哪些属性？如何为原型对象增加属性？  
  以第一题中的代码为例，Person/Person prototype/person1/person2间的关系如图所示。  
  ![构造函数、实例、原型对象关系图](../../res/pic/6_3_1.jpg)  
  原型对象包含了构造函数中的一系列属性。  
  在最开始时，原型对象仅拥有一个constructor属性，该属性指向Person类。  
  在Person中，先后通过Person.prototype.xx为其增加了name、age和sayName三个属性。  
  在person1和person2中，两个对象实例均有一个指向Pesron Prototype的指针(ES5中称为[[Prototype]])。  
  调用他们的sayName时，实际上是通过该指针调用了Person Prototype(原型对象)中的方法。  

3. 原型模式中，实例可通过指针获取构造函数中原型对象的数据，给实例增加属性时，是否会影响到原型对象？  
    ```
    function Person(){
    }
    Person.prototype.name = "Nic";
    Person.prototype.age = 29;
    Person.prototype.sayName = function() {
        console.log(this.name);
    }
    
    var person1 = new Person();
    person1.sayName();  //Nic
    
    var person2 = new Person();
    person2.sayName();  //Nic

    person1.name = "Jack";
    
    console.log(person1.sayName()); //Jack
    console.log(person2.sayName()); //Nic
    ```  
  重设person1的name属性后，新的关系图如下图所示。  
  ![构造函数、实例、原型对象关系图](../../res/pic/6_3_2.jpg)  
  执行```person1.name = "Jack"```实际上是给person1新增的一个属性。  
  访问person1.name时，直接在person1中找到了属性name，打印出Jack。  
  访问person2.name时，person2没有name属性，通过[[Prototype]]找到了对象原型中的name，打印出Nic。  
