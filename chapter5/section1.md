# 第一节 Array类型
1. 创建Array实例的两种方法及区别？  
  答：var arr = new Array(arrLength)/var arr = Array(arrLength)和var arr = [...]。  
  需要注意的是第二种方法中应尽量避免出现未赋值的项。  
  比如var values=[1, 2, ]，这种情况在不同浏览器中会造成不同的结果。在IE8及其之前的版本中会创建一个[1, 2, undefined]的数组，在其他浏览器中会创建一个[1, 2]的数组。
  
2. Array的length属性可写吗？  
  答：可写。  
  写入的length大于数组的长度时，会在数组之后添加相应个undefined。  
  写入的length小于数组的长度时，会截断数组在length之后的值。  
  如：
    ```
    var arr = [1, 2, 3, 4, 5];
    arr.length = 6;
    console.log(arr[5]);    //undefined
    arr.length = 3;
    console.log(arr[4]);    //undefined
    ```  
  此外，利用length属性，可以方便的在数组的末尾添加项：  
    ```
    var arr = [];
    for(var i = 0 ; i < 100 ; i++){
        arr[arr.length] = i;
    }
    //执行完成后的arr为：[0, 1, ..., 99]  
    ```
3. 如何确定某对象是否为数组？  
  答：对于一个网页/全局作用域，使用instanceof即可完成判断-```console.log(values instanceof Array)```。  
  然后使用instanceof的前提是只用一个全局执行环境。更好的方法是使用ES5中提供的方法isArray:```console.log(Array.isArray(values))```  
  
4. 介绍一下数组中的reverse/sort方法？  
  答：reverse()用于反转数组项的顺序，sort会默认调用数组中各项的toString方法并比较各项的字符串大小，按照该大小进行排序。例：  
    ```
    var arr = [2, 5, 10, 1];
    arr.sort();
    console.log(arr); //[1, 10, 2, 5]
    ```  
  注意，由于sort默认__对数组中各项的toString的结果按大小进行排序__，因此使用该方法对全数字组成的数组进行排序时会与期望出现偏差。此时可以重新指定sort排序的参照标准：  
    ```
    function compare(v1, v2){
        return v1 - v2;
    }
    arr.sort(compare);
    console.log(arr); //[1, 2, 5, 10]
    ```  
  传递给sort的比较函数接受两个参数，sort对数组进行排序时对各项调用该比较函数。  
  比较arr[x]与arr[y]时，若compare(arr[x], arr[y])返回负数，则将arr[x]置于arr[y]之前，若返回正数则调换顺序。  
  
5. 介绍一下数组中的splice方法？  
  答：splice(begin, count, [item1, item2, ...])。  
  数组调用该函数，从arr[begin]开始删除count个项，并在arr[begin]之后插入(item1, item2, ...)。  
  该函数中count的数量可以为0，可灵活使用该函数可以完成增(```arr.splice(insertBeginIndex, 0, insertItem)```)、删(```arr.splice(deleteBeginItem, count)```)、改(```arr.splice(oldItemIndex, 0, newItem)```)等功能。  
  
6. 介绍一下数组中的迭代/归并方法？  
  答：迭代方法：  
  1. every(): 对数组中的每一项运行给定函数，若该函数对数组的每一项均返回true，则返回true。  
  2. some(): 对数组中的每一项运行给定函数，若该函数对数组的其中一项返回true，则返回true。  
  3. filter(): 对数组中的每一项运行给定函数，返回该函数会返回true的项组成的数组。  
  4. forEach(): 对数组中的每一项运行运行给定函数，该方法无返回值。  
  5. map(): 对数组中的每一项运行给定函数，返回每次函数调用的结果组成的值。  
    ```
    var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1];
    
    var everyResult = numbers.every(function(item, index, array) {
        return (item > 2);
    });
    console.log(everyResult);   //false
    
    var someResult = numbers.some(function(item, index, array) {
        return (item > 2);
    });
    console.log(someResult);    //true
    
    var filterResult = numbers.filter(function(item, index, array) {
        return (item > 2);
    })
    console.log(filterResult);  //[3, 4, 5, 4, 3]
    
    var mapResult = numbers.map(function(item, index, array) {
        return item * 2;
    });
    console.log(mapResult);     //[2, 4, 6, 8, 10, 8, 6, 4, 2]
    
    numbers.forEach(function(e) {
        console.log(e);         //print each element in numbers
    }); 
    ```
  归并方法：  
  reduce()/reduceRight()：迭代数组的所有项并返回最终值。  
  reduce()从数组的第一项遍历至最后一项，reduceRight()遍历顺序相反。  
    ```
    var numbers = [1, 2, 3];
    var sum = numbers.reduce(function(prev, cur, index, array) {
        return prev + cur;
    });
    console.log(sum);           //6
    ```