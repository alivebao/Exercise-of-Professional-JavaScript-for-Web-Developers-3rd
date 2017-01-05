# 第二章 在HTML中使用JavaScript

1. script元素

  1.1 简介script定义的6个属性？    
    答：async, charset, defer, language, src, type
    * async: 可选，表示以异步的方式立即下载该脚本
    * charse: 可选，表示该脚本的字符集。大多浏览器会忽略该值，因此该属性很少被使用
    * defer: 可选，表示该脚本可延迟至文档被完全解析和显示后再执行
    * language: 已废弃，无使用必要
    * src: 可选，表示包含要执行代码的外部文件
    * type: 可选，表示飙血代码使用的脚本语言的内容类型，及MIME类型，默认为text/javascript
    
  1.2 使用<srcipt>引入外部脚本的写法是？
    
    答：可以写成<script src=”...”></script>或<script src=”...” />, 但需要注意的是不能在HTML文档中使用第二种写法(XHTML中可以)。因为该种语法不符合HTML规范，且某些浏览器无法正确解析(如IE)。