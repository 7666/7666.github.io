---
layout: post
title:  "JAVAScript入门"
date:   2017-08-15 08:16:54
categories: JAVAScript
tags: JAVAScript
---

* content
{:toc}

JAVAScript一种直译式脚本语言,是一种动态类型.弱类型.基于原型的语言,内置支持类型.
它的解释器被称为JAVAScript引擎,为浏览器的一部分,广泛用于客户端的脚本语言,最早是在HTML网页上使用,用来给HTML网页增加动态功能.




### 组成部分

* ECMAScript,描述了该语言的基本语法.
* 文档对象模型(DOM),描述处理网页内容的方法和接口.
* 浏览器对象模型(BOM),描述与浏览器进行交互的方法和接口.

![](http://oujvmc3la.bkt.clouddn.com/js.jpg)

### 基本特点

JAVAScript是一种属于网络的脚本语言,已经被广泛用于Web应用开发,常用来为网页添加各种各样的动态效果,为用户提供更流畅美观的浏览效果.通常JAVAScript脚本是通过嵌入在HTML中来实现自身的功能的.

1. 是一种解释性脚本语言(代码不进行预编译).
2. 主要用来向HTML页面添加交互行为.
3. 可以直接嵌入HTML页面,但写成单独的js文件有利于结构和行为的分离.
4. 跨平台特性,在绝大多数浏览器的支持下,可以在多种平台下运行(如windows.Linux.Mac.Android.ios等)

### JAVAScript的作用

* 嵌入动态文本与HTMLyemain
* 对浏览器事件做出响应.
* 读写HTML元素.
* 在数据被提交到服务器之前验证数据.
* 检测访客的浏览器信息
* 控制cookies,包括创建和修改等.
* 基于Node.js技术进行服务器编程

### JAVAScript的编写方式

* 行内样式

    `<button onclick="alert();">点我</button>`

* 嵌套样式:这个样式是写在`<body></body>`之内的,而不是别的.

```
<!--嵌套javascript  -->
  <script>
    alert("我是提示框！！！！");
  </script>
```
* 外部的js脚本

  先要创建一个`.js`结尾的文件,在里面写你需要的js脚本.
  然后同样是在`<body></body>`标签中引入外部js脚本.
  `<script src="./text.js"></script>`

### javascript 基本概念

#### 严格区分大小写

第一个概念就是ECMAScript中的一切(变量,函数名和操作符)都区分大小写.
这也就意味着,变量名`test`和变量名`Test`分别代表着两个不同的变量.而函数名不能使用`typeof`,因为他是一个关键字,但`typeOf`则完全可以是一个有效的函数名.

#### 标识符

所谓标识符,就是指变量,函数,属性的名字,或者函数的参数.标识符可以使按照下列格式规则组合起来的一个或多个字符:

1. 第一个字符必须是一个字母,下划线(_)或一个美元符号($)其他字符可以是字母,下划线,美元符号或数字.

2. 标识符的字母也可以包含扩展的ASCII或Unicode字母字符,但我们不推荐这么做.

3. 按照惯例,ECMAScript 标识符采用驼峰大小写格式,也就是第一个字母小写,剩下的每个单词的首字母大写,例如:`firstChild`
4. 不要和关键字重名

#### 注释风格

1. 单行注释`//`,`//这里是单行注释!`

2. 多行注释`/* 这是注释内容! */`

```
/*
这里是注释!
*/
```

> 注意:不要和python,html中的注释混淆.

#### 语句

ECMAScript 中的语句以一个分号结尾;如果省略分号,则由解析器确定语句的结尾,比如:

```
var value1 = a - b  //不推荐
var value2 = a + b; //推荐
```

使用代码块,让代码看起来更加清晰,比如:

```
//不推荐
if (value)
  alert("value is ...")

//推荐
if (value){
  alert("value is ...")
}
```

#### 关键字

![](http://oujvmc3la.bkt.clouddn.com/keywords.png)

> 注意:定义标识符时不要使用关键字和保留字.

### JAVAScript 变量

ECMAScript 的变量是松散类型的,所谓松散类型就是可以用来保存任何类型的数据.换句话说,每个变量仅仅是一个用于保存值的占位符而已.定义变量时要使用`var`操作符.再次定义变量就不需要`var`操作符了.
比如:

```
//定义变量！！！！
    // var是个关键字，a是变量名(标识符)
    //注意标识符的命名规则
    var a = 10; //分号表示一条语句的结尾

    //用于控制台输出
    console.log(a);
```

### JAVAScript 数据类型

ECMAScript 中有 5 种简单数据类型(也称为基本数据类型): `Undefined`, `Null`, `Boolean`, `Number`和 `String` 。
对一个值使用 `typeof` 操作符可能返回下列某个字符串:

* “undefined” ——如果这个值未定义;
* “boolean” ——如果这个值是布尔值;
* “string” ——如果这个值是字符串;
* “number” ——如果这个值是数值;
* “object” ——如果这个值是对象或 null ;
* “function” ——如果这个值是函数。

例如:

```
var a = "string";
 alert(typeof a); //string

 var b = 123;
 alert(typeof b); //number

 var c = true;
 alert(typeof c);//boolean

 var d;
 alert(typeof d);//undefined

 var f = function(){alert("hello");};
 alert(typeof f);//function

 var e = null;
 alert(typeof e);//object    
```

#### 字符串类型

String 类型用于表示由零或多个 16 位 Unicode 字符组成的字符序列,即字符串。字符串可以由双引号(")或单引号(’)表示,因此下面两种字符串的写法都是有效的:

```
var a = "string1";
var b = 'string2';
```

> 注意:不要混合使用单引号或者双引号,要统一,否则会报错.

```
var str1 = "hello";
     var str2 = "world";
     var str3 = 'hehe';
     console.log(str1,str2,str3);
     console.log("10");

    //typeof 测试数据类型
    console.log(typeof str1);//string

    //再次使用变量时，不需要var
    str1 = "HELLO";
    console.log(str1);

    //字符串拼接 "+"
    var  newStr = str1 + str2;
    console.log(newStr);


    //其他类型如何转换为字符串, toString()!!!!
    a = 20;
    console.log(a.toString());//直接变为字符串
    console.log(a.toString(2));//将数字按照2进制转换为字符串， 10100

```
