#### JavaScript简介

> 历史
  
    1995年 Netscape 一位名为 Brendan Eich 的工程师创造了 Javascript
    1996年 首先被应用在 Netscape2 浏览器上
    1997年 ECMAScript 标准第一版诞生
    1999年 ECMAScript 第三版
    2009年 ECMAScript 第五版
    2015年 ECMAScript 第六版
  
> 概览
  
    JavaScript 是一种多范式动态语言，它包含类型、运算符、标准内置(built-in)对象和方法。
    JavaScript 通过原型链而不是类来支持面向对象编程。支持函数式编程。  

> 类型
 
   + 基础数据类型（值不可变、不可以添加属性和方法、简单赋值、值比较、存在栈区）
     - Number（数字）
     - String（字符串）
     - Boolean（布尔）
     - Null（空）
     - Undefined（未定义）
     - Symbol（符号）
     
   + 引用数据类型（值可变、可以添加属性和方法、赋值是对象引用、引用的比较、同时存在栈区和堆区中）
     - Object
       * Array
       * Function
       * Date
       * RegExp
        
> 运算符
    
    JavaScript 的运算符包括 +、-、*、/、 %(求余)、==、=== 等等
    
   + 相等(==)运算符：

         会为两个不同类型等操作数转换类型，然后进行严格比较。
         当两个操作数都是对象时，JavaScript会比较其内部引用，当且仅当他们的引用指向内存中
         相同对象（区域）时才相等，即他们在栈内存中的引用地址相同。
    