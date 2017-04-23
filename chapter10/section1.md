# 第一节 节点层次
1. 什么是DOM？  
  DOM(文档对象模型)是针对HTML和XML稳定的一个API，其描绘了一个层次化的节点树，允许开发人员添加、移除和修改页面的某一部分。  
2. 什么是文档元素？  
  文档元素是文档的最外层元素，文档中的其他所有元素都包含在文档元素中。  
  每个文档只能有一个文档元素，在HTML中，文档元素始终都是<HTML>元素。  
3. JS中所有节点类型都继承自Node类型，因此所有节点类型都共享着相同的基本类型和方法。列举常见的Node类型？
  Node.ELEMENT_NODE(1)/Node.ATTRIBUTE_NODE(2)/Node.TEXT_NODE(3)...
4. 每个节点都有一个childNodes属性，其中保存着一个NodeList对象，该对象与数组的关系？  
  NodeList是一种用于保存一组有序节点的类数组对象，。虽然可以通过方括号语法访问NodeList的值，且该对象也有length属性，但__该对象并不是Array的实例__。   
  NodeList实际上是基于DOM结构动态执行查询的结果，DOM结构的变化自动反映(注意，是自动反映，不是快照)在NodeList对象中。
5. 常用的Node类型节点操作方法？  
  操作某个节点的子节点的方法：  
    appendChild: someNode.appendChild(newNode); //在someNode节点的末尾添加newNode节点。如果newNode已经是someNode的一部分，则直接将newNode节点从原位置置于someNode的末尾，返回值为插入的节点。  
    insertBefore: someNode.insertBefore(newNode, someNode.firstChild); //将newNode插入至someNode的第一个子节点。当第二个参数为null时与appendChild功能相同，返回值为插入的节点。  
    replaceChild: someNode.replaceChild(newNode, someNode.lastChild); //替换someNode的最后一个子节点  
    removeChild: someNode.removeChild(someNode.firstChild); //删除someNode的第一个子节点  
  所有类型都有的方法：  
    cloneNode(boolean): 参数为true时执行深复制，否则执行浅复制。  
    normalize: 处理文档树中的文本节点-在调用该方法的节点的后代节点中执行操作：删除空文本节点，合并相邻的文本节点。