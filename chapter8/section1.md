# 第一节 window对象
1. 什么是BOM，与DOM有什么区别？  
  BOM(Browser Object Model, 浏览器对象模型)提供了许多用于访问浏览器功能的对象，这些功能与网页内容无关。BOM没有相关标准，最根本的对象是window。  
  DOM(Document Object Model, 文档对象模型)和文档有关，这里的文档指的是__网页__。DOM和浏览器无关，关注的是网页本身的内容。DOM是W3C标准，最根本的对象是document。  
  
2. 什么是window对象？  
  window是BOM的核心对象，表示一个浏览器实例。浏览器中的window对象及时通过JS访问浏览器窗口的一个窗口，又是ECMASciprt规定的Global对象。也就是说，在网页中定义的任何一个对象、变量和函数，都以window作为其全局对象。  
  
3. 什么是窗口的框架(frame)?  
  如果页面中包含框架，则每个框架都拥有自己的window对象，且保存在frames集合中。例：  
    ```
    <html>
        <head>
            <title>Frameset Example</title>        
        </head>
        <frameset rows="160, *">
            <frame src="frameTop.html" name="topFrame">
            <frameset cols="50%, 50%">
                <frame src="frameLeft.html" name="leftFrame">
                <frame src="frameRight.html" name="rightFrame">            
            </frameset>
            </frame>
        </frameset>
    </html>
    ```  
  在最高层窗口中通过代码访问框架的方式如图所示：  
  ![作用域链](../../res/pic/8_1_1.jpg)  
  __在使用框架的情况下，浏览器中会存在多个Global对象。每个框架中定义的全局变量会自动称为框架中的window对象的属性。__  
  
4. 如何获取窗口位置？  
  screentLeft/screenTop & screenX/screenY(Opera)。  
    ```
    var leftPos = (typeof window.screenLeft == "number" ? window.screenLeft : window.screenX);
    var topPos = (typeof window.screenTop == "number" ? window.screenTop : window.screenY);
    ```  
  __在IE/Opera中，screenLeft和screenTop中保存的是从屏幕坐标和上边到由window对象表示的页面可见区域的距离__  
  __在Chrome/Firefox/Safari中，screenY/screenTop中保存的是整个浏览器窗口对于屏幕的坐标值。__  
  
5. 如何获取浏览器页面视口大小？不同浏览器下innerWidth/outerWidth和innerHeight/outerHeight的区别？  
    ```
    //获取页面视口大小
    var pageWidth = window.innderWidth;
    var pageHeight = window.innerHeight;
    
    if(typeof pageWidth != "number) {
        if(document.compatMode == "CSS1Compat"){    //判断页面是否处于标准模式
            pageWidth = document.documentElement.clientWidth;
            pageHeight = document.documentElement.clientHeight;        
        }
        } else {
            pageWidth = document.body.clientWidth;
            pageHeight = document.body.clientHeight;
        }
    }
<table>
  <tbody>
    <tr>
      <th align="center"></th>
      <th align="center">IE9+</th>
      <th align="center">Firefox</th>
      <th align="center">Safari</th>
      <th align="center">Opera</th>
      <th align="center">Chrome</th>
    </tr>
    <tr>
      <td align="center">outerWidth/outerHeiht</td>
      <td align="center">浏览器本身尺寸</td>
      <td align="center">浏览器本身尺寸</td>
      <td align="center">浏览器本身尺寸</td>
      <td align="center">页面视图容器的大小</td>
      <td align="center">视口大小</td>
    </tr>    
    <tr>
      <td align="center">innerWidth/innerHeight</td>
      <td align="center">不支持</td>
      <td align="center">?</td>
      <td align="center">?</td>
      <td align="center">该容器页面中页面视图区的大小(减去边框宽度)</td>
      <td align="center">视口大小</td>
    </tr>    
  </tbody>
</table>

6. setTimeout和setInterval的区别？  
  setTimeout接受两个参数-要执行的代码和以毫秒表示的时间。第一个参数可以是一个包含JS的字符串，也可以是一个函数。  
  setTimeout返回一个id，在setTimeout中的代码执行前可通过clearTimeout(id)取消尚未执行的调用计划：  
    ```
    var timeoutId = setTImeout(function() {
        alert("Hello");
    }, 3000);
    
    clearTimeout(timeoutId)；
    ```  
  setInterval类似与setTimeout，不同之处在于setTimeout只执行一次，setInterval在调用clearInterval前会不断执行。  
  一般认为使用超时调用(setTimeout)模拟间歇调用(setInterval)是一种最佳模式，最好不要使用间歇调用。  
  