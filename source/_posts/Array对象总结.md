title: Array对象总结
date: 2016-04-02 14:34:32
tags:
  - js
  - note
categories:
  - 前端
---

## 概述

`Array对象`用于在单个的变量中存储多个值。

## 创建

* `new Array()` 返回一个空数组，length字段为0
* `new Array(size)` 返回一个非空数组，其元素为size个undifined
* `new Array(ele0,ele1,ele2,...,elen)`返回一个非空数组，其元素为`ele0,ele1,ele2,...,elen`
* `Array()` 将其作为函数调用时，效果与使用new运算符将其当做构造函数来调用时的效果一样
* `[ele0,ele1,ele2,...,elen]` 当然这样用是最常用的

## 属性

* `constructor` 返回对创建次对象的数组函数的引用
* `length` **设置**或返回数组中元素的数目
* `prototype` 向`Array对象`添加属性和方法

其中，值得注意的是`length`属性，不仅可以取得当前`Array对象`中元素的数目，也可以设置当前`Array对象`可以容纳元素的数目，如果设置其length值小于当前的对象的元素数目，则会删去超出长度的元素。

```
let arr = new Arrary(1,2,3);
console.log(arr.length, arr);
arr.length = 2;
console.log(arr.length, arr);
//2 [1, 2]
arr.length = -1;
//invalid array length
```

## 方法

主要分为3类：

* 数组操作
* 数组递归
* 数组查找
* 数组遍历

### 数组操作

|方法|描述|
|:--|:--|
|`concat()`|在原`Array对象`的基础上连接新的`Array对象`，返回一个新的`Array对象`，和`String对象`的`concat()`实现类似功能|
|`copyWithin(target,start,end)`|在`Array对象`内进行复制，从start位置开始，在end（缺省为数组尾）位置*前*结束，复制到target位置，溢出忽略|
|`fill(value,start,end)`|在`Array对象`内进行批量赋值，从start位置（缺省为0）开始，在end（缺省为数组尾）位置*前*结束|
|`Array.isArray()`|判断一个数组是否是`Array对象`|
|`join(separator)`|将数组中元素间隔着separator连接为一个字符串|
|`pop()`|删除数组中最后一个元素，返回该元素|
|`push()`|在数组尾中存入若干个元素（多个参数），返回元素的长度|
|`reverse()`|逆序数组，改变数组值，返回该数组|
|`shift()`|删除数组中第一个元素，，返回该元素|
|`slice(start,end)`|取数组中start到end（缺省为元素尾，不包括）之前的元素，负值表示从元素尾取值|
|`sort(compareFunction)`|缺省按字符串的字符升序排序，compareFunction为递归函数，返回值负值者在前|
|`splice(index,howmany,item1,.....,itemX)`|若howmany为0则在index位置开始插入，若howmany为正则从index开始删除后在index位置开始插入。因此可以在数组中任意位置插入，删除（无item）元素|
|`toString()`|相当于`join(',')`|
|`unshift()`|在数组头插入元素|
|`valueOf()`| `numbers === numbers.valueOf()` // `true`|

### 数组递归

|方法|描述|
|:--|:--|
|`reduce(function(total,currentValue,currentIndex,arr),initialValue)`|按照function从左到右递归该数组，total为上一次递归函数的返回值（初始值为数组第一个元素，即第一次递归是元素1和元素2之间的操作），currentValue为当前递归的数组元素，currentIndex当前递归元素的索引，arr为该数组|
|`reduceRight()`|与`reduce()`相同，从右往左|

### 数组查找

|方法|描述|
|:--|:--|
|`find(function(currentValue,index,arr),thisValue)`|返回第一个符合function（返回值为true）的元素，find会跳过空值的元素（定义但未赋值），返回值为该元素|
|`findIndex()`|与find类似，返回值为元素的索引|
|`indexOf(searchElement[, fromIndex = 0])`|查元素，返回第一次出现的索引，searchElement要查找的元素，fromIndex开始查找的位置。如果该索引值大于或等于数组长度，意味着不会在数组里查找，返回-1。如果参数中提供的索引值是一个负值，则将其作为数组末尾的一个抵消，即-1表示从最后一个元素开始查找，-2表示从倒数第二个元素开始查找 ，以此类推。 注意：如果参数中提供的索引值是一个负值，仍然从前向后查询数组。如果抵消后的索引值仍小于0，则整个数组都将会被查询。其默认值为0.|
|`lastIndexOf()`|返回从右往左第一次出现的索引|

### 数组遍历

|方法|描述|
|:--|:--|
|`filter(function(currentValue,index,arr), thisValue)`|遍历数组，currentValue为当前元素，index为当前元素索引，arr为数组对象，thisValue为function内this值，缺省*取决于当前执行环境是否为严格模式（严格模式下为 undefined，非严格模式下为全局对象*（见[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach))|
|`forEach()`|对数组中每个元素进行操作，且无法跳出循环，不改变数组的值|
|`map()`|对数组中每个元素进行操作，且无法跳出循环，将返回值组成一个新的数组返回|
|`some(function)`|全部不通过function返回false|
|`every(function)`|全部通过function返回true|
