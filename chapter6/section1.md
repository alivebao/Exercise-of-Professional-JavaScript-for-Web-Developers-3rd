# 第一节 理解对象
1. ES中有数据属性和访问器属性两种属性，介绍一下数据属性中描述其行为的4个特性-Configurable/Enumerable/Writable/Value？  
  答：  
  1. [[Configurable]]：表示能否通过delete删除属性从而重新定义属性，能否修改属性的特性，或能否把属性特性修改为访问器属性。直接在对象上定义的属性，该值默认为true。
  2. [[Enumerable]]：表示能否通过for-in循环返回属性。直接在对象上定义的属性，该值默认为true。
  3. [[Writable]]：表示能否修改属性的值。直接在对象上定义的属性，该值默认为true。
  4. [[Value]]：包含这个属性的数据值。读取属性值时，从该位置读；写入属性值时，将新值保存在该位置。这个特性的默认值为undefined。  
  想要修改属性的默认值，必须使用ES5的Object.defineProperty(objName, attrName, descriptor)。  
  将Writable/Configurable设为false后，尝试更新/删除属性的值时，非严苛模式下，操作不生效。严苛模式下，系统报错。  
  
2. 介绍一下访问器属性中的4个特性-Configurable/Enumerable/Get/Set?  
  答：  
  1. [[Configurable]]和[[Enumerable]]与数据属性中的Configurable/Enumerable类似。
  2. [[Get]]：在读取属性时调用的函数，默认值为undefined。
  3. [[Set]]：在写入属性时调用的函数，默认值为undefined。  
  
  同数据属性一样，想要修改属性的默认值，必须使用ES5的Object.defineProperty(objName, attrName, descriptor)。  

  
