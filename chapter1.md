# 第一章 JavaScript简介

1. JavaScript的组成部分？
答：如图所示，一个完整的JavaScript由以下三部分组成：
    1. 核心(ECMAScript) - 由ECMA-262定义，与web浏览器没有依赖关系。我们常见的web浏览器只是ECMAScript实现可能的宿主环境之一。ECMA-262是一种脚本语言标准，致力于解决JavaScript标准化问题，定义了语言的语法、类型等基础规范。ECMAScript可以看作是对实现ECMA-262标准的语言的描述，JavaScript/JScript等都是ECMAScript的一种实现。
    2. 文档对象模型(DOM) - 用于操作HTML元素的API。HTML由各种类型的节点组成，DOM将其解析为树结构(如图所示)，并提供API访问/修改该树。
        1. DOM1 - 由DOM核心(规定基于XML文档结构的映射标准)和DOM HTML(在DOM核心的基础上扩展，添加了针对HTML的对象和方法)组成。
        2. DOM2 - 在原DOM基础上扩充了鼠标和用户界面事件、返回、遍历(迭代DOM文档的方法)等细分模块，且通过对象接口增加了对CSS的支持。
        3. DOM3 - 进一步扩展了DOM，引入了以同一方式加载和保存文档的方法，新增了验证文档的方法等。同时对DOM核心进行了扩展，开始支持XML 1.0规范。
    3. 浏览器对象模型(BOM) - 开发者可以使用BOM控制浏览器显示的页面以外的部分。