# 第三节 创建对象-原型模式
1. 什么是prototype属性？简单介绍一下函数的prototype属性。  
  答：我们所创建的每个函数都有一个prototype属性，该属性是一个指针，指向一个__原型对象__，该函数的所有实例都可以通过prototype共享其属性和方法：  
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
  答：以第一题中的代码为例，Person/Person prototype/person1/person2间的关系如图所示。  
  ![构造函数、实例、原型对象关系图](../../res/pic/6_3_1.jpg)  
  原型对象包含了构造函数中的一系列属性。  
  在最开始时，原型对象仅拥有一个constructor属性，该属性指向Person类。  
  在Person中，先后通过Person.prototype.xx为其增加了name、age和sayName三个属性。  
  在person1和person2中，两个对象实例均有一个指向Pesron Prototype的指针(ES5中称为[[Prototype]])。  
  调用他们的sayName时，实际上是通过该指针调用了Person Prototype(原型对象)中的方法。  

3. 原型模式中，实例可通过指针获取构造函数中原型对象的数据，给实例增加属性时，是否会影响到原型对象？  
  答：不会。  
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
  当为对象实例添加一个新属性时，这个属性就会__屏蔽__原型对象中保存的同名属性。  
  执行```person1.name = "Jack"```实际上是给person1新增的一个属性。  
  访问person1.name时，直接在person1中找到了属性name，打印出Jack。  
  访问person2.name时，person2没有name属性，通过[[Prototype]]找到了对象原型中的name，打印出Nic。  
  
4. in操作符有什么作用(仅需说明单独使用的情况，不需说明for-in中的in)？与hasOwnProperty有何区别？  
  答：单独使用时，in操作符会在通过对象能够访问给定属性时返回true，__无论该属性存在与实例中还是原型中__。  不同于in，__hasOwnProperty(attr)仅在属性存在于实例时返回true__。  
  利用这两个方法可以判断出属性是属于实例还是原型：  
    ```
    if("name" in Person){
        if(person.hasOwnProperty("name")){
            console.log("name is in person");
        } else{
            console.log("name is in Person");
        }
    } else{
        console.log("name is not in Person")
    }
    ```  
  
5. 谈谈纯原型模式的缺点？  
  1. 省略了未构造函数传递初始化参数的过程。  
  2. prototype中所有属性都是被多个实例共享的。这种共享对函数非常合适，对包含基本值的属性(对实例相应的属性"重新"赋值后会直接为实例增加该属性)，__但是__，对于__包含引用类型值的属性__，则存在极大的问题：  
    ```
    function Person(){
    }
    Person.prototype = {
        ...
        friends: ["Alice", "Jack", "Snobby"]
    }
    var person1 = new Person();
    var person2 = new Person();
    
    person1.friends.push("Van");
    
    console.log(person1.friends);   //"Alice, Jack, Snobby, Van"
    console.log(person2.friends);   //"Alice, Jack, Snobby, Van"
    ```  
  可以看到的是person1中对friends修改后，person2的friends也会反应出来(这是因为person1.friends和person2.friends均是通过指向prototype的指针指向了Person.prototype的属性, 实际上指向的是同一个属性-Person.prototype.friends)  
6. 如何解决原型模式的缺点？  
  答：可以采用组合使用构造函数模式和原型模式的方法解决该问题-实例属性在构造函数中定义，所有实例共享的属性和方法在原型中定义：  
    ```
    function Person(name, age){
        this.name = name;
        this.age = age;
        this.friends = {"A", "B"};
    }
    Person.prototype = {
        constructor: Person,
        sayName: function() {
            console.log(this.name);
        }
    }
    
    var person1 = new Person("Nic", 29);
    var person2 = new Person("Ger", 23);
    
    person1.friends.push("C");
    
    console.log(person1.friends);   //"A, B, C"
    console.log(person2.friends);   //"A, B"
    ```
