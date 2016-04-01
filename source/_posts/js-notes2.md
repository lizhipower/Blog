title: "对象基础"
date: 2015-05-08 14:43:38
tags: [js,note]
---

##定义
* 对象：属性的无序结合，每个属性存放一个原始值、对象或者函数。每个对象由类定义，定义了对象的接口（开发者访问的属性和方法），内部工作（使属性和方法发挥作用的代码）。
* 实例：程序使用类创建对象时，生成的对象叫做类的实例。每个实例的行为相同，但是实例处理一组独立的数据。创建过程叫做实例化。
* ECMA-262类：类是对象的配方。
* ECMA-262对象：对象由特性（attribute）构成，特性可以是原始值，也可以是引用值，如果特性存放的是函数，它将被看作对象的方法，否则该特性被看错属性。
* 引用类型：通常叫作类。在ECMAScript中，不能访问对象的物理表示，只能访问对象的引用。每次创建对象，存储在变量中的都是该对象的引用，而不是对象本身。


    var a = {c:1, b:2}
    c = a
    c.c=2
    c
    Object {c: 2, b: 2}
    a
    Object {c: 2, b: 2}
所以在对于对象的操作，比如复制中，会遇到深度复制这样的问题，要确保复制的不是引用。

##对象的类型
###本地对象
* Array
主要方法有：
1. `join`、`split`、`slice`、`pop`、`shift`、`push`，Array对象的动作像一个栈，是后进先出的。通过`shift`、`push`可以使Array对象有队列一样的动作。
2. `sort`、`reverse`与数组项的顺序有关。`reverse`使数组倒序，`sort`根据数组项的值升序为他们排序。`sort`是将所有值转化为字符串，然后根据自负代码比较数组项，可以通过`sort（obj,fun(){}）`设置排序规则来进行排序。
3. `splice`用来把数据项插入数组中部，可以用来：删除`arr.splice(0,2)`、插入`arr.splice(2,0,"insertContent")`、替换`arr.splice(2,1,"replaceContent")`。

* Date
Date类对UTC日期和时间有很强的依赖性，需要考虑时区、夏时令等情况。并且覆盖了`valueOf`、`toString`方法。

###内置对象

定义：由ECMAScript实现提供的、独立于宿主环境的所有对象，在ECMAScript程序开始执行时出现。ECMA-262定义了两个内置对象，即Global和Math。

* Global

Global实际上根本不存在。Global几个比较重要的方法有`encodeURI`系列，用来处理URI；`eval`用来吧参数解释为真正的ECMAScript语句，操作Json时候用到过。
另外，**在ECMAScript中不存在独立的函数，所有函数都必须是某个对象的方法**。

###宿主对象

定义：所有非本地对象都是宿主对象。

* this
this用在对象的方法中，关键字this总是只想调用该方法的对象。通过this可以在任意多个地方重用同一个函数。

##定义类或对象

###工厂方式

    function createCar() {
        var oTempCar = new Object;
        oTempCar.color = "red";
        oTempCar.showColor = function() {
            console.log(this.color)
        };
        
        return oTempCar;
    }
    
    var oCar1 = createCar();
     
这样可以通过调用函数来创建新对象，但是每个对象都会有一个版本的`showColor`，因此需要通过原型方式来进行定义类。

###构造函数方式

    function Car() {
        this.color = "red";
        this.showColor = function() {
            console.log(this.color)
        };
        
    }
    
    var oCar1 = new Car();
    
同样地，也会重复生成函数。

###原型方式

    function Car() {
        this.prototype.color = "red";
        this.prototype.showColor = function() {
            console.log(this.color)
        };
        
    }
    
    var oCar1 = new Car();
在调用`new Car()`时，原型的所有属性都被赋予也要创建的对象，也就是说所有的Car实例存放的都是指向`showColor（）`的指针。然而，由于都是指向同一个位置，如果改变某个实例的属性，其他所有实例的该属性都会改变。因此需要混合构造函数/原型方式来进行创建对象。

###混合方式

    function Car() {
        this.color = "red";
    }
    Car.prototype.showColor = function() {
        console.log(this.color)
    };
    
##对象修改
通过`prototype`可以创建新方法，重新定义已有方法。