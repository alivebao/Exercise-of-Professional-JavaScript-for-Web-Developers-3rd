# 第一节 能力检测&怪癖检测
1. 什么是能力检测(又称为特性检测)?  
  能力检测是最常用也最为人们广泛接受的客户端检测形式。  
  其目标不是识别特定的浏览器，而是识别浏览器的能力。  
  比如，IE5.0之前不支持document.getElementById()方法，要获取DOM时可采用类型下面的能力检测代码：  
    ```
    function getElement(id){
        if(document.getElementById){
            return document.getElementById(id);
        } else if (document.all) {
            return docuement.all[id];
        }
    }
    ```  

2. 什么是怪癖检测(quirks detection)？  
  怪癖检测的目标是识别浏览器的特殊行为。是想要知道浏览器存在什么缺陷。  
  
3. 能力检测与怪癖检测的区别？  
  能力检测: 确认浏览器支持什么能力  
  怪癖检测: 检测浏览器存在什么bug