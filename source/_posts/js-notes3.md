title: "继承"
date: 2015-05-10 12:49:41
tags: [js,note]
---

##对象冒充

原理：构造函数使用this关键字给所有属性和方法赋值（采用类声明的构造函数方式）。以为构造函数只是一个函数，可以使ClassA的构造函数成为ClassB的方法，然后调用它。ClassB就会收到ClassA的构造函数中定义的属性和方法。这里，其实是把ClassA作为常规函数来建立继承机制，而不是作为构造函数。需要注意的是，所有的新属性和新方法都必须在删除了新方法之后定义，否则，新属性和新方法可能会被继承到的属性和方法覆盖。

并且，对象冒充可以支持多重继承，同样的，如果继承的不同类中存在相同的方法和属性，也会存在前者被后者被覆盖的问题。

随着对象冒充的流行，ECMAScript为Function对象加入了`call()`和`apply()`。

* `call()`
`call()`的第一个参数是obj，说明`fun.call(obj,arg1,arg2)`的`fun()`中的this关键字的值是obj，这样就可以将`call()`和对象冒充结合起来，将对象冒充的中赋值、调用和删除替换掉。

        function ClassB(sColor, sName) {
            //this.newMethod = ClassA;
            //this.newMethod(sColor);
            //delete this.newMethod;
            ClassA.call(ClassB,sColor);
        
            this.name = sName;
            this.sayName = function()｛
                console.log(this.name);
            ｝;
        }        
        
* `apply()`
`apply()`方法有两个参数，用作this的对象和要传递给函数的参数的数组。

##原型链

原理：prototype对象是一个模板，要实例化的对象都是以这个模板为基础，prototype对象的任何属性和方法都被传递给那个类的所有实例。原型链利用这种功能来实现继承机制。

        function ClassA() {
        };
        
        ClassA.prototype.color = "red";
        
        function ClassB() {
        };
        
        **ClassB.prototype = new ClassA();**
        
与对象冒充相似，子类的所有属性和方法必须出现在prototype属性被赋值后，因为prototype属性被替换成了新对象。
原型链的弊端是不支持多重继承，prototype会被覆盖。

## 混合方式
创建类的最好方式是用构造函数方式定义属性，用原型方式定义方法，同样，对于继承，也是用对象冒充继承构造函数属性，用原型链继承函数的方法。