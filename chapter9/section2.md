# 第二节 用户代理检测
1. 什么是用户代理检测？  
  用户代理检测通过检测用户代理字符串来确定实际使用的浏览器。  
  在每一次HTTP请求过程中，用户代理字符串是作为响应首部发送的，该字符串可通过JS的navigator.userAgent属性访问。  
  在服务器端，通过该放手确定用户使用的浏览器是一种常用且广为接受的方法。  
  在客户端，其优先级排在能力检测/怪癖检测之后。  

2. 介绍一下常见的浏览器及内核？  
  浏览器: IE/Safari/Chrome/Chromium/Opera/Firefox  
  引擎: Trident(IE内核)/Gecko(Firefox内核)/Webkit(Safari内核,Chrome内核原型)/Presto(早期opera内核,7.0~12.16, 之后Opera采用WebKit)
  
3. 如何识别内核？  
  顺序: Opera -> WebKit -> KHTML -> Gecko -> MSIE
  1. 首先应该识别Opera，因为其用户代理字符串有可能完全模仿其他浏览器。可以通过检测window.opera对象识别Opera，Opera5及更高版本中都有这个对象。
    ```
    if(window.opera){
        engine.ver = window.opera.version();
        engine.opera = parseFloat(engine.ver);
    }
    ```    
  2. 检测WebKit。WebKit中包含"Gecko"和"KHTML"，先检测这两个字符串可能会得到错误结论。WebKit的用户代理字符串中的“AppleWebKit”是独一无二的，可以通过检测该对象确定WebKit。
    ```
    var ua = navigator.userAgent;
    if(window.opera){
        ...
    } else if (/AppleWebKit\/(\S+)/.test(ua)){
        engine.ver = RegExp["$1"];
        engine.webkit = parseFloat(engine.ver);
    }
    ```  
  3. 检测KHTML。KHTML的用户代理字符串中也包含"Gecko"，在排除KHTML之前无法准确检测基于Gecko的浏览器。KHTML的版本号与WerKit的版本号在用户代理字符串中的格式类似。  
    ```
    var ua = navigator.userAgent;
    if(window.opera){
        ...
        //opera
    } else if (/AppleWebKit\/(\S+)/.test(ua)){
        ...
        //webkit
    } else if (/KHTML\/(\S+)/.test(ua) || /Konqueror\/([^;]+)/.test(ua)){
        //KHTML
    }
    ```  
  4. Gecko & IE ...