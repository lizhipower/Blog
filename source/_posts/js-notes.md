title: "ECMAScript基础"
date: 2015-04-23 15:50:21
tags: [js,note]
---
#ECMAScript基础
##原始类型
1. 原始类型有Undefined、Null、Bollean、Number和String。
2. typeof用来判断一个值是否在某种类型的范围内，引用类型或者Null返回object，null被认为是对象的占位符。
3. undefined： 
    - 声明的对象未初始化
    - 对象未定义：**只能对未定义的对象使用typeof，使用其他运算符会报错**
    - 函数无明确返回值
4. null用于表示尚未存在的对象。
5.  `typeof(1)`和`typeof(NaN)`都是`number`，但`isNaN(NaN)`与`isNaN(1)`是不一样的。
6. Number的`toString()`可以根据不同的基输出结果。
7.  String的`pasreInt()` 可以把字符串中的第一串数字字符转化成数字（0xA会被转化成10），会在第一个无效字符之前停止，同样也有基模式。

##引用类型
1. String可以有`indexof()`、`charAt()`、`valueOf()`、`toString()`等方法。
2. String的`slice()`可以传负参数，其表示字符串长度加上负参数值，slice开始位置包含在返回值，终止位置不包含在返回值，从0开始计位置。

##函数
1. js的函数不支持重载，但是可以使用特殊对象arguments，无需指出参数名，就能访问它们。ECMAScript不会验证传递给函数的参数个数是否等于函数定义的参数个数，其中，遗漏的函数以undefined传递给函数，多余的参数被忽略，因此可以通过arguments来简易模拟函数重载。
`function a() {}`等价于`var a = function(){}`。
2. 函数实际上是功能完整的对象。Function类可以表示开发者定义的任何函数。**函数名实际上是函数对象的引用值**，**函数可以作为参数传递给另外一个函数**。
3. **闭包**

 **闭包**是指函数能使用函数外定义的变量。


    <!--lang:javascript--> 
    var iBaseNum = 10;
    function addNumbers(iNum1, iNum2) {
        //闭包
        function doAddition (){
            return iNum1 + iNum2 + iBaseNum;
        }
    return doAddition();
    } 

 闭包可以用来读取局部变量。

    function f1(){
        var n=999;
        function f2(){
           alert(n); // 999
        }
    }

    function f1(){
        var n=999;
        function f2(){
            alert(n); 
        }
        return f2;//返回函数的引用
    }
    var result=f1();// result =  f2
    result(); // 999

 [闭包](http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html "学习Javascript闭包")主要用来**读取函数内部的变量**或者**让这些变量的值始终保持在内存中**。个人认为，闭包的关键在于返回了一个子函数，子函数可以调用父函数的变量，从而可以再外部调用到父函数内部的变量。这里的子函数如果是定义为全局变量，则直接通过调用子函数来实现访问内部变量。
