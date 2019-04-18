
    我就想知道,你们项目里面是不是很少用到原型相关知识?

### 一.数据类型

 #### 动态类型

 JavaScript是一种弱类型,并且是动态语言.所以你不用提前声明数据类型,而在程序运行的过程中,数据的类型会被自动确认.简单的说,一个同一个变量
 也可以改变数据类型.

 #### 概念

 (1). 堆（heap）是没有结构的，数据可以任意存放，它是用于存放复杂数据类型（引用类型）的，例如数组对象、object对象等。

 (2). 栈（stack）是有结构的，每个区块按照一定次序存放（后进先出），栈中主要存放的是基本类型的变量的值以及指向堆中的数组或者对象的地址，
 存在栈中的数据大小与生存期必须是确定的。除此之外，还可以明确知道每个区块的大小。

 (3). js中基本数据类型的值不可变,也就是说基本数据类型的值的改变是重新再赋值.

 (4). 原始值的比较是值的比较

  用 const 定义的变量是不能改变的，这里其实分两种情况：如果定义的是基本数据类型的变量，那么的确是不能对其做任何操作来改变其值的；但如果定义
  的是引用类型的变量，这个变量存储的其实只是一个地址，也就是说我们不能改变的是这个地址，但是地址中的内容我们还是可以改变的。

 #### 数据类型

 (1). 原始数据类型(基本数据类型):存储在栈

  * Boolean

   任意的JavaScript的值都可以转换为布尔值。undefined,null, 0,-0,NaN,""这6个值,再加上false本身共7个值都会转换为false

  * Null

    在这里要说明的是：在JavaScript中，null是基础数据类型，但是typeof判断为object，这是由于历史原因造成的。
    在JavaScript最初的实现中，JavaScript中的值是由一个表示类型的标签和实际数据值表示的。对象的类型标签是0。由于null代表的是空指针(大多数平台下值为0x00），
    因此，null使用0作为类型标签，typeof null就返回了”object”。

  * Undefined

  当声明的变量未初始化时,该变量的默认值为undefined.

  * Number

  可以用来表示进制数,浮点数等.还有一个特殊的值NaN,一般来说出现这种值的时候是发生类型转换失败的时候,例如把不带'a'转化成数字,并且NaN也不等于自己本身.
  可以用Number.isNaN()或者 isNaN() 来判断是否为NaN.

  * String

  String类型也是基本数据类型,并且不可被修改,只能被覆盖.

  * Symbol (ES6)

  符号(Symbols)是ECMAScript 6新定义的,Symbol()函数返回symbol类型的值,都是唯一的,不相等的,并且具有静态属性和静态方法.
  symbol值可以用来作为对象属性的标识符,这是Symbol数据类型的唯一目的.

 (2). Object类型:存储在堆

  * Object

  * Array

  * Date

  * RegExp

  * Function

  注意 typeof(new Function()) 返回function

  #### 函数

  (1). 函数对象概念

  所有typeof返回'function'的对象都是函数对象.

  函数对象与其他用户所定义的对象有着本质的区别,这一类对象被称之为内部对象,例如日期对象(Date)、数组对象(Array)、字符串对象(String)都属于内部对象.
  这些内置对象的构造器是由JavaScript本身所定义的:通过执行new Array()这样的语句返回一个对象,JavaScript内部有一套机制来初始化返回的对象,
  而不是由用户来指定对象的构造方式.

  ```
  alert(typeof(Function)));             //function
  alert(typeof(new Function()));        //function
  alert(typeof(Array));                 //function
  alert(typeof(Object));                //function
  alert(typeof(new Array()));           //object
  alert(typeof(new Date()));            //object
  alert(typeof(new Object()));          //object

  let fun = function () {};
  console.log(typeof(fun));             //function
  console.log(typeof(new fun()));       //object
  ```

  可见new一个function实际上是返回一个函数.这与其他的对象有很大的不同.其他的类型Array、Object等都会通过new操作符返回一个普通对象.
  尽管函数本身也是一个对象,但它与普通的对象还是有区别的,因为它同时也是对象构造器,也就是说,可以new一个函数来返回一个对象（typeof( new fun())
  返回一个object对象）,这在前面已经介绍.所有typeof返回“function”的对象都是函数对象.也称这样的对象为构造器（constructor）,因而,
  所有的构造器都是对象,但不是所有的对象都是构造器.

  (2). 函数的apply、call方法 与 bind.

  * JavaScript为函数对象定义了两个方法:apply和call,它们的作用都是将函数绑定到另外一个对象上去运行,两者仅在定义参数的方式有所区别:

    Function.prototype.apply(thisArg,argArray);

   ```
   function log(){
     console.log.apply(console, arguments);
   };
   log(1);    //1
   log(1,2);    //1 2
   ```

    Function.prototype.call(thisArg[,arg1[,arg2…]]);

  从函数原型可以看到,第一个参数都被取名为thisArg,即所有函数内部的this指针都会被赋值为thisArg,这就实现了将函数作为另外一个对象的方法运行的目的.


    bind()方法会创建一个新函数，称为绑定函数，当调用这个绑定函数时，绑定函数会以创建它时传入 bind()方法的第一个参数作为 this，传入 bind() 方法的
    第二个以及以后的参数加上绑定函数运行时本身的参数按照顺序作为原函数的参数来调用原函数。

 * apply、call、bind比较

 ```
 var obj = {
    x: 81,
 };

 var foo = {
    getX: function() {
        return this.x;
    }
 }

 console.log(foo.getX.bind(obj)());  //81
 console.log(foo.getX.call(obj));    //81
 console.log(foo.getX.apply(obj));   //81
 ```

 也就是说，区别是，当你希望改变上下文环境之后并非立即执行，而是回调执行的时候，使用 bind() 方法。而 apply/call 则会立即执行函数。

 * apply 、 call 、bind 三者都是用来改变函数的this对象的指向的；
 * apply 、 call 、bind 三者第一个参数都是this要指向的对象，也就是想指定的上下文；
 * apply 、 call 、bind 三者都可以利用后续参数传参；
 * bind 是返回对应函数，便于稍后调用；apply 、call 则是立即调用 。