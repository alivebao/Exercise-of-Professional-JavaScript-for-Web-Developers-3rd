# 第二节 location/navigator和history对象
1. location对象常用的属性有哪些？  
  1. host - 返回服务名称和端口号(如果有)
  2. hostname - 返回不带端口号的服务器名称
  3. href - 返回当前加载页面的完整URL  
  4. pathname - 返回URL中的目录和(或)文件名  
  5. port - 返回端口号  
  6. protocol - 返回页面使用协议  
  7. search 返回URL的查下字符串，该字符串以问号开头  
  
2. 常用的改变浏览器href的方法有哪些？这些方法与replace的区别？  
    ```
    var link = "http://www.xx.com"
    
    location.assign(link);
    window.location = link;
    location.href = link;
    ```  
  使用上述方式修改URL，浏览器的历史记录中会生成一条新记录，可以通过点击后台返回到前一个页面。  
  使用replace方法不会在历史记录中生成新的记录，而是直接替换当前页面，用户无法回到前一个页面。  

3. navigator对象的主要作用是？  
  检测浏览器类型，如浏览器版本号、浏览器是否安装某特定插等。

4. history对象的常用函数？  
    ```
    history.go(x);
    // x > 0 - 前进x页
    // x < 0 - 后退x页
    history.back();     //相当于history.go(-1)
    history.forward();  //相当于history.go(1)
    ```    