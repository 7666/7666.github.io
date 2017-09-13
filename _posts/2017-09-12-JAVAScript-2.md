---
layout: post
title:  "JAVAScript基础进阶"
date:   2017-09-12 08:16:54
categories: JAVAScript
tags: JAVAScript
---

* content
{:toc}

JavaScript声明提升
JavaScript数值转换
javascript操作符及控制语句
javascript函数传参
javascript函数操作符
javascript数组的应用
javascript原生DOM操作
javascript原生事件操作







## 声明提升

### 变量声明提升

变量声明提升:变量的定义在执行时会被提升到当前作用域的顶部，但是赋值的操作位置不变.

实例:

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>javascript</title>
  </head>
  <body>
    <script type="text/javascript">

    console.log(f);//undefined
    var f = 100;
    /*
    变量声明提升:变量的定义在执行时会被提升到当前作用域的顶部，但是赋值的操作位置不变
    */
    </script>
  </body>
</html>
```

### 函数声明提升

函数声明提升：会将函数的声明提升到当前作用域的顶部.    

实例:

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>作用域</title>
  </head>
  <body>

    <script type="text/javascript">
    fun();//100

    // 函数声明提升：会将函数的声明提升到当前作用域的顶部
    function fun(){
      var f = 100;
      console.log(f);
    }

    </script>

  </body>
</html>
```

### 经典面试题

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>提升</title>
  </head>
  <body>

    <script type="text/javascript">

    var a = 10;

    function fun(){
      console.log(a);//undefined
      var a = 100;

      /*等价代码*/
      /*
      var a;
      console.log(a);//undefined
      a = 100;
      */
    }

    fun();//

    </script>

  </body>
</html>
```

这个题,局部可以调用全局变量,所以应该会显示10.这是错的.不要忘了后面还有个`var a = 100;`,变量声明提升,所以`var a;`被提升到了局部的最顶部,所以全局变量a在局部被局部变量a覆盖了,由于变量声明提升,只有声明,没有赋值,所以这里的a为`undefined`.

## 数值转换

有3个函数可以把非数值转换为数值:`Number()`,`parseInt()`和`parseFloat()`.   

### Number()

`Number()`可以用于任何数据类型,若该类型不能被装换为数字,则返回`NaN`.       
实例:

```
var num1 = Number("Hello world!"); //NaN
var num2 = Number("");//0
var num3 = Number("000011");//11
var num4 = Number(true);//1
var num5 = Number(false);//0
var num6 = Number("123hello");//NaN
var num7 = Number("0x12");//10
```

### parseInt()

`parseInt()`函数在转换字符串时,更多的是看其是否符合数值模式.它会忽略字符串前面的空格,直到找到第一个非空格字符.如果第一个字符不是数字字符或者负号,`parseInt()`就会返回`NaN`;也就是说,用`parseInt()`转换空字符串会返回`NaN`(`Number()`对空字符串返回的是0).    
如果第一个字符是数字字符,`parseInt()`会继续解析第二个字符,直到解析完所有后续字符或者遇到了一个非数字字符.     
例如:`123hello`会被转换为`123`,因为`hello`会被完全忽略.类似的,`22.5`会被转换为`22`,因为小数点并不是有效的数字字符.  

```
console.log(parseInt(""));//NaN
console.log(parseInt("1234abc"));//1234
console.log(parseInt("abc"));//NaN
console.log(parseInt("10.123"));//10
console.log(parseInt("0x12"));//18
console.log(parseInt("070"));//70, 并没有解析为８进制
```

为了消除在使用`parseInt()`函数时可能导致的进制转换问题,可以为这个函数提供第二个参数,转换时使用的基数(即多少进制).也就是说这个只能由别的进制转换为10进制,而不能将10进制转换为其他的进制.

```
console.log(parseInt("010", 8));
console.log(parseInt("10", 2));
console.log(parseInt("20",2));//超过范围时，转换为NaN
console.log(parseInt("10", 10));
console.log(parseInt("10", 16));
```

### parseFloat()

`parseFloat()`函数也是从第一个字符开始的(位置0)开始解析每个字符,都按照十进制解析.而且也是一直解析到字符串的末尾,或者解析遇见一个无效的浮点数字字符为止.      
也就是说,字符串中的第一个小数点是有效的,而第二个小数点就是无效的了,因此他后面的字符串将被忽略.

```
console.log("----parseFloat---------");
console.log(parseFloat("10.234")); //10.234
console.log(parseFloat("10.abc"));//10
console.log(parseFloat("10.23.4"));//10.23
console.log(parseFloat("0x10.234"));//0
console.log(parseFloat("010.234"));//10.234
console.log(parseFloat("abc"));//NaN
```

## 操作符以及控制语句

### break和continue

`break`和`continue`语句用于在循环中精确的控制代码的执行.其中,`break`语句会立即退出循环,强制继续执行循环后面的语句.而`continue`语句虽然也是立即退出循环,但退出循环后会从循环的顶部继续执行.

> `break`只会跳出一层循环.`continue`后面的的语句不会执行.

```
for(var i = 0; i < 10; i++){
    if (i == 5){
       break;
     }
    alert(i);
  }

  for (var i = 0; i < 5; i++){
    if (i < 5){
      continue;
    }
    alert(i);
  }
```

如果是多层循环,你想用`break`跳出所有的循环,就必须用到`label`语句,使用`label`语句可以在代码中添加标签,以便将来使用.

实例:

```
out: for (var j = 0; j < 10; j++) {

    console.log("j = " + j);

    for (var i = 0; i < 10; i++) {
      console.log("i = " + i);
      if (i == 5) {
        //跳出当前循环，继续运行循环后边的代码
        // break;

        //跳出指定循环，继续运行循环后边的代码
        break out;
      }
    }
  }
```

在这里`break`跳出的就不仅仅是一层循环了,而是跳出了`label`语句标记的循环.

### switch语句

`switch`语句与if语句的关系最为密切,而且也是在其他语言中普遍使用的一种流控制语句.    
`switch`语句中使用任何数据类型(在很多其他语言中只能使用数值),无论是字符串,还是对象都没有问题.其次,每个`case`的值不一定是常量,可以是变量,甚至可以是表达式.      

```
switch(expression) {
  case value1:
       statement
       break;
   case value2:
       statement
       break;
   default:
       statement
       break;
}
```

> 注意要使用关键字`break`,否则会导致执行多个`case`语句.不过有些特殊情况也需要忽略`break`以实现某个目标.
没有`break`会导致,匹配到一个`case`,他后面的`case`也会依次执行.

实例:是一个输入日期,求该该天是今年的第多少天?

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>

    <script type="text/javascript">
    var year = 2017, mon = 10, day = 10;
    var leap = 0, sum = 0;

    if ((year % 400 == 0) || ((year % 4 == 0) && (year % 100 != 0))){
      leap = 1;
    }

    switch (mon){
      case  12:
      sum += 30;
      case  11:
      sum += 31;
      case  10:
      sum += 30;
      case  9:
      sum += 31;
      case  8:
      sum += 31;
      case  7:
      sum += 30;
      case  6:
      sum += 31;
      case  5:
      sum += 30;
      case  4:
      sum += 31;
      case  3:
      sum += 28 + leap;
      case  2:
      sum += 31;
      case  1:
      sum += day;
    }

    console.log(sum);
    </script>

  </body>
</html>
```

### JAVAScript函数

函数对于任何编程语言来说都是一个核心的概念.通过函数可以封装任意多条语句,而且可以在任何地方.任何时候调用执行.

```
javascript函数示例:
function sum(arg1,arg2){
  return arg1 + arg2;
}
sum(1,2)
```

在上面的代码中,其中`arg1`,`arg2`为传递的形参,`sum(1,2)`中的数值为实参.

#### arguments对象

`arguments`是存储了函数传递过来的实参的,并且arguments对象只有函数开始时才可用.`arguments`对象只是与数组类似(它并不是ARRAY的实例),因为可以使用方括号语法访问它的每一个元素(即第一个元素是`arguments[0]`,第二个元素是`arguments[1]`,依次类推),使用`length`属性来确定传递进来多少个参数.     

实例:

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>函数传递参数</title>
  </head>
  <body>

    <script type="text/javascript">

//参数个数随意
     //arguments 是一个伪数组
     function sum(arg){

      //arguments只能在函数内部使用！！！！！
      //arguments 用于获得实参
       console.log(arguments);

       var result = 0;

       //arguments.length是参数的个数
       for (var i = 0; i < arguments.length; i++) {
         //arguments[i], 就指定参数
         result += arguments[i];
       }
       console.log(result);
     }

     console.log(sum.length);//1
     //该函数的形式参数个数！！！！！！

     sum();
     sum(1);
     sum(1,2);
     sum(1,2,3);

         </script>

       </body>
     </html>

```

#### 函数返回值

函数调用一次之后表示运算完毕,使用return关键字可以返回结果,同样return可以提前结束函数的运行.

```
function fun(arg1,arg2){
  return arg1 + arg2;
  console.log("after return ...");//不会执行
}
fun();//返回计算结果

function fun1(arg1){
  console.log(arg1);
  return;//返回undefined
}
```

### 布尔操作符

布尔操作符一共有3个:与,非,或.

#### 逻辑非(!)

```
alert(!false); //true
alert(!"blue");//false
alert(!0);//true
alert(!NaN);//true
alert(!"");//true
alert(!12345);//false
```

#### 逻辑与(&&)

操作符由两个和号(&&)表示,至少有两个操作数.      
逻辑与的特点：短路     
短路：与运算从左向右执行，一旦遇到一个为假的,那么后边的不再执行      

```
console.log(10 && 0);//0
console.log(0 && 10);//0
console.log(10 && 20);//20
console.log(10 && true);//true
console.log(10 && false);//false

var d = 10;

//d++本身是一个表达式，只不过该表达式的值等于 没有自增1之前的值。
//++d本身也是一个表达式,只不过该表达式的值等于自增1以后的值.
console.log(10 && 20 && 30 && d++);//10
console.log(d);//11

```

#### 逻辑或(||)

操作符由两个竖线符号(||)表示,至少有两个操作数.    
它的特点和逻辑与类似,也是短路,不过他是从左向右执行,一旦遇到一个为真,那么后面的不在执行.   

```
console.log(10 || false);//10
console.log(false || 10 || 20 );//10
```

### 关系操作符

小于(<),大于(>),小于等于(<=),和大于等于(>=),相等(==)，不等(!=)，全等(===)，不全等(!==)操作符.

1. 如果两个操作数都是数值,则执行数值比较.
2. 如果两个操作数都是字符串,则比较两个字符对应的字符编码值.
3. 如果一个操作数是数值,则将另一个操作数转换为一个数值,然后执行数值比较.
4. 如果一个操作数是对象,则调用这个对象的`valueOf()`方法,用得到的结果按照前面的规则执行比较.如果对象没有`valueOf()`方法,则调用`toString()`方法,并用得到的结果根据前面的规则执行比较.
5. 如果一个操作数是布尔值,则现将其转换为数值,然后再执行比较.

```
console.log(10 > 20);//false
console.log(10 < 20);//true
console.log(10 < "23");//true
console.log("23" > "233");//false,按照编码的大小去比较,它是挨个字符去比较.

console.log(10 > NaN);//false
console.log(10 < NaN);//false
console.log(10 == NaN);//false
console.log(NaN == NaN);//false


/*
==  相等, 是先转换再比较
=== 全等, 是仅比较而不转换
*/

console.log(10 == "10");//true
console.log(10 === "10");//false

console.log(10 != "10");//false
console.log(10 !== "10");//true

```

### 三目运算符

`var result = 表达式１? 表达式2: 表达式3;`      
如果表达式１的值为true, 那么表达式2的值会赋值给result;否则，表达式3的值会赋值给result.

```

// 如果表达式１的值为true, 那么表达式2的值会赋值给result;否则，表达式3的值会赋值给result
    var result = 10 > 20 ?  'hello' : 'world';
    console.log(result);//world

    /*
    if (10>20){
    result = 'hello';
    } else {
    result = 'world';
    }
    */
```

### 复合操作符

复合操作符用于简化操作符,提升性能.

```
//复合运算符
var a = 10, b = 20;
a += b; // a = a + b;
a -= b; // a = a - b;
a *= b; // a = a * b;
a /= b; // a = a / b;
a %= b; // a = a % b;
```

### 逗号操作符

使用逗号操作符可以在一条语句中执行多个操作,如下所示:     
`var num = 1, num1 = 2;`      

逗号操作符还可以用于赋值.在用于赋值时,逗号操作符总会返回表达式中的最后一项,比如:    
`var result = (表达式1,表达式2,表达式3);`    
result的值为表达式3的值.逗号运算符取最后一个的结果为整个表达式的结果,但是前边所有的表达式都会运算.

## JAVAScript数组

数组是值的有序集合,每个值就是一个元素,每个元素在数组中有一个位置,以数字表示,成为索引.JAVAScript数组是无类型,数组元素可以是任意类型,并且同一个数组中的不同元素也可能是不同的类型.

```
var  one = [];
console.log(typeof one);//object
```

### 创建数组

使用数组直接量进行创建,方括号中使用逗号隔开:

```
var a = [];
var b = [10,2,3];
var c = [1.1,true,'a'];
var d = [1,2,,3];  //其中省略的元素值为undefined,稀疏数组
```

使用Array()创建:

```
var a = new Array();//创建空数组
var b = new Array(10);//创建长度为10的元素
var c = new Array(1,2,3);//创建一个已经包含三个元素的数组
```

### 数组的读写操作:

```
var a = ["hello"];
var b = a[0];
a[1] = "world";
i = 1;
a[i + 2] = "string";
```

### 数组的长度:

```
var a = [1,2,3,4];
console.log(a.length); //长度为４

a[999] = 999; //长度为　1000, 稀疏数组的长度大于元素的个数
console.log(a.length);// 长度为1000
```

### 数组的遍历

使用for循环是最常见的遍历数组的方式:

```
var a = [1,2,3,4,5,6];
for(var i = 0; i < a.length; i++){
  console.log(a[i]);
}
//这里还是可以提高效率的!如下:
for(var i = 0, len = a.length; i < len; i++){//这里把长度赋值,不用每次去调用这个方法.
  console.log(a[i]);
}
```

更简单的方式:

```
for (var i in a){
  console.log(a[i]);
}
```
使用一个方法`forEach()`也是可以遍历的,后面会说到.

## 数组常用的方法

### 数组元素的添加和删除

添加:

- 直接对新索引值进行赋值(不是一个方法).
- `push()`使用`push()`方法在数组末尾添加一个或者多个元素.返回值为新长度.
- `unshift()`使用`unshift()`方法在数组的开端添加一个或者多个元素.

删除:

- 直接用delete删除,如:`delete a[0];`,他不会改变元素的索引位置和长度,只是把那个元素变为`undefined`.
- `pop()`删除最后一个值,长度减一.返回值为删除的那个元素.
- `shift()`方法从数组中删除第一个元素，并返回该元素的值。此方法更改数组的长度。

实例:

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>数组的添加和删除</title>
  </head>
  <body>

    <script>
    // 直接对新索引值进行赋值
    var a1 = [1,2,3];
    a1[3] = 4;
    a1[4] = 5;

    //直接用delete删除
    delete a1[0];//不影响长度

    //末尾的添加，删除
    console.log(a1.push(10,20,30));//8
    console.log(a1);//[undefined,2,3,4,5,10,20,30]

    //删除最后一个，长度减1
    console.log(a1.pop());//30

    //开头添加，删除
    //shift unshift
    var a2 = [1,2,3,4,5];
    console.log(a2.shift());//1

    // a2.unshift(10,20,30);
    a2.unshift(10);
    a2.unshift(20);
    a2.unshift(30);
    console.log(a2);//[30,20,10,2,3,4,5]
    </script>

  </body>
</html>
```

### join()方法

`join()`方法,数组拼接,不会改变原有数组,只是将拼接的字符串作为返回值,默认用`,`拼接.

```
var a2 = [1,2,3,4,5,6];
//join 数组拼接
console.log(a2.join());//1,2,3,4,5,6
console.log(a2.join(''));//123456
console.log(a2.join('*'));//1*2*3*4*5*6
console.log(a2.join('+'));//1+2+3+4+5+6
console.log(a2);//[1,2,3,4,5,6],可见原有数组并不会发生改变
```

### reverse()方法

`reverse()`颠倒方法,将数组中元素的位置颠倒。第一个数组元素成为最后一个数组元素，最后一个数组元素成为第一个。reverse 方法颠倒数组中元素的位置，并返回该数组的引用。

```
//reverse颠倒，数组本身也被修改了
var a4 = ['h', 'e', 'l', 'l', 'o'];
console.log(a4.reverse());//['o', 'l', 'l', 'e', 'h']
console.log(a4.reverse());//['h', 'e', 'l', 'l', 'o']
```

### sort()方法,对数组进行排序

`sort()`方法在适当的位置对数组的元素进行排序，并返回数组。 sort 排序不一定是稳定的。默认排序顺序是根据字符串Unicode码点。   
参数为一个函数,如果没有参数,默认按`unicode`码进行排序.

```
var a9 = [10,2,3,80];
    console.log(a9.sort());//按照字符的编码进行排序，默认从小到大,比较的是第一个字符.

    // sort传入参数进行排序
    a9.sort(function(a,b){
      console.log("a = %d, b = %d", a, b);

      //从小到大排序为a-b,从大到小排序为b-a
      return a - b;
    });

    //影响原数组
    console.log(a9);
```

### concat方法，连接数组并返回一个新数组

`concat() `方法用于合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组。

```
var num1 = [1, 2, 3];
var num2 = [4, 5, 6];
var num3 = [7, 8, 9];
// 组成新数组[1, 2, 3, 4, 5, 6, 7, 8, 9]; 原数组 num1, num2, num3 未被修改
var nums = num1.concat(num2, num3);



var alpha = ["a", "b", "c"];
var numeric = [1, 2, 3];
// 组成新数组 ["a", "b", "c", 1, 2, 3]; 原数组 alpha 和 numeric 未被修改
var alphaNumeric = alpha.concat(numeric);
```

### slice 方法，对数组内容进行浅复制

`slice()`方法返回一份从开始到结束(不包括结束)选择的数组的一部分浅拷贝到一个新数组对象.原始数组不会被改变.     
两个参数:分别为开始位置和结束位置.都是可选参数.返回值为一个含有提取元素的新数组.

```
//slice 数组切片
   var a12 = [1,2,3,4,5,6,7,8,9,10];

   //begin end(不包含)
   console.log(a12.slice(1,4));//[2,3,4]
   console.log(a12.slice());//全切
   console.log(a12.slice(3));//从3开始切，到最后
   console.log(a12.slice(-7,8));//从4开始。。。。。

   var result = a12.slice(0,3);
   result[0] = 100;
   //result, a12不是同一块内存地址，相互不影响
   console.log(a12, result);



   //slice浅复制(引用类型)
   var a13 = [[100,200,300],1,2,3,4,5];
   result = a13.slice(0,3);

   //修改切片后的数组
   result[0][0] = 1000;
   console.log(a13, result);//互相影响,引用的是同一块内存地址.
```

### splice　对数组元素进行替换修改

splice() 方法通过删除现有元素和/或添加新元素来更改一个数组的内容。   

语法:

- array.splice(start)
- array.splice(start, deleteCount)
- array.splice(start, deleteCount, item1, item2, ...)

参数:

- start​:指定修改的开始位置（从0计数）。如果超出了数组的长度，则从数组末尾开始添加内容；如果是负值，则表示从数组末位开始的第几位（从1计数）。
- deleteCount 可选 :整数，表示要移除的数组元素的个数。如果 deleteCount 是 0，则不移除元素。这种情况下，至少应添加一个新元素。如果 deleteCount 大于start 之后的元素的总数，则从 start 后面的元素都将被删除（含第 start 位）。如果deleteCount被省略，则其相当于(arr.length - start)。
- item1, item2, ... 可选:要添加进数组的元素,从start 位置开始。如果不指定，则 splice() 将只删除数组元素。

返回值:

由被删除的元素组成的一个数组。如果只删除了一个元素，则返回只包含一个元素的数组。如果没有删除元素，则返回空数组。

```
/*
splice: 添加，删除，修改
*/
var myFish = ["angel", "clown", "mandarin", "surgeon"];
result = myFish.splice(0,1);//result，删除元素组成的数组
console.log(myFish,result);//['angel']

//任意位置添加
myFish.splice(1,0,"hello", "world");
console.log(myFish);//["clown","hello", "world","mandarin", "surgeon"]

//修改
myFish.splice(2,1, "china");
console.log(myFish);//["clown","hello", "china","mandarin", "surgeon"]
```

### toString()

`toString()` 返回一个字符串，表示指定的数组及其元素。与`join()`类似.但是他没有参数,只能以`,`连接.

```
var monthNames = ['Jan', 'Feb', 'Mar', 'Apr'];
var myVar = monthNames.toString(); // assigns "Jan,Feb,Mar,Apr" to myVar.
```

### ECMA5中数组新方法

#### array.forEach()

`array.forEach(callback[, thisArg])`

callback 在数组每一项上执行的函数，接收三个参数：

- currentValue, 当前项（指遍历时正在被处理那个数组项）的值。
- index, 当前项的索引（或下标）。
- array, 数组本身。
- thisArg 可选参数。用来当作callback 函数内this的值的对象.

>  forEach在遍历完数组元素之前是不会终止的.

```
// forEach直接遍历
var a14 = [1,2,3,4,5,6,7,8];
var sum = 0;

// 直接遍历
a14.forEach(function(current,index, arr){
  console.log("current = ", current);
  // console.log("index = ", index);
  // console.log("arr = ", arr);
  sum += current;
});
console.log(sum);
```

#### array.map()

`array.map(callback[, thisArg])`

callback 在数组每一项上执行的函数，接收三个参数：

- currentValue, 当前项（指遍历时正在被处理那个数组项）的值。
- index, 当前项的索引（或下标）。
- array, 数组本身。
- thisArg 可选参数。用来当作callback 函数内this的值的对象。

返回值： 一个由原数组中的每个元素调用一个指定方法后的返回值组成的新数组

```
// for (var i = 0; i < a14.length; i++) {
//   a14[i] += 10;
// }

//map 等价于上面的函数
var result = a14.map(function(current,index,arr){

  //map需要每次返回，由返回的数据共同组成一个新数组
   return current + 10;
});
console.log(result);
```

#### indexOf()

`arr.indexOf(searchElement[, fromIndex = 0]) `

- searchElement   要查找的元素        
- fromIndex     指定开始位置,默认为0  

返回给定元素能找在数组中找到的第一个索引值，否则返回-1。  

```
var a15 = [10,20,30,20,80,60,34];
console.log(a15.indexOf(20));//1
console.log(a15.indexOf(200));//-1
```
