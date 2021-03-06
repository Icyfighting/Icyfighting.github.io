---
layout: post
title: "Java Generic learning"
subtitle: "Generic class & Generic method & Generic interface"
author: "Bing Yan"
header-img: "img/generic/post-bg-java.jpg"
header-mask: 0.2
catalog: true
tags:
  - Java
  - Generic
  - Learning
---
## 前言
Java 泛型（generic）是 JDK 5 中引入的一个新特性, 泛型提供了编译时类型安全检测机制，该机制允许程序员在编译时检测到非法的类型。
泛型的本质是参数化类型，也就是说所操作的数据类型被指定为一个参数。
一提到参数，最熟悉的就是定义方法时有形参，然后调用此方法时传递实参。那么参数化类型怎么理解呢？顾名思义，就是将类型由原来的具体的类型参数化，类似于方法中的变量参数，此时类型也定义成参数形式（可以称之为类型形参），然后在使用/调用时传入具体的类型（类型实参）。


## 正文
### 泛型的好处
*   类型安全
>泛型的主要目标是提高 Java 程序的类型安全。通过知道使用泛型定义的变量的类型限制，编译器可以在一个高得多的程度上验证类型假设。没有泛型，这些假设就只存在于程序员的头脑中（或者如果幸运的话，还存在于代码注释中）。

*   消除强制类型转换
>泛型的一个附带好处是，消除源代码中的许多强制类型转换。这使得代码更加可读，并且减少了出错机会。

*   潜在的性能收益
>泛型为较大的优化带来可能。在泛型的初始实现中，编译器将强制类型转换（没有泛型的话，程序员会指定这些强制类型转换）插入生成的字节码中。但是更多类型信息可用于编译器这一事实，为未来版本的 JVM 的优化带来可能。由于泛型的实现方式，支持泛型（几乎）不需要 JVM 或类文件更改。所有工作都在编译器中完成，编译器生成类似于没有泛型（和强制类型转换）时所写的代码，只是更能确保类型安全而已。


### 泛型的规则和限制

 1. 泛型的类型参数只能是类类型（包括自定义类），不能是简单类型。
 2. 同一种泛型可以对应多个版本（因为参数类型是不确定的），不同版本的泛型类实例是不兼容的。
 3. 泛型的类型参数可以有多个。
 4. 泛型的参数类型可以使用extends语句，例如<T extends superclass>。习惯上成为“有界类型”。
 5. 泛型的参数类型还可以是通配符类型。例如Class<?> classType = Class.forName(Java.lang.String);


### 泛型使用分类
泛型使用可以分为泛型接口、泛型类、泛型方法。


**泛型接口（Generic interface）**
定义一个泛型接口：<br/>
 ![](/img/generic/interface-1.png) 
通过类去实现这个泛型接口的时候指定泛型T的具体类型。
指定具体类型为Integer:<br/>
 ![](/img/generic/interface-2.png)
指定具体类型为String:<br/>
 ![](/img/generic/interface-3.png)

**泛型类（Generic class）**
泛型类的声明和非泛型类的声明类似，除了在类名后面添加了类型参数声明部分。
和泛型方法一样，泛型类的类型参数声明部分也包含一个或多个类型参数，参数间用逗号隔开。一个泛型参数，也被称为一个类型变量，是用于指定一个泛型类型名称的标识符。因为他们接受一个或多个参数，这些类被称为参数化的类或参数化的类型。
![](/img/generic/class-1.png)

**泛型方法（Generic method）**
定义泛型方法的规则：
*   所有泛型方法声明都有一个类型参数声明部分（由尖括号分隔），该类型参数声明部分在方法返回类型之前（在下面例子中的<E>）。
*   每一个类型参数声明部分包含一个或多个类型参数，参数间用逗号隔开。一个泛型参数，也被称为一个类型变量，是用于指定一个泛型类型名称的标识符。
*   类型参数能被用来声明返回值类型，并且能作为泛型方法得到的实际参数类型的占位符。
*   泛型方法体的声明和其他方法一样。注意类型参数只能代表引用型类型，不能是原始类型（像int,double,char的等）。
  
下面的例子演示了如何使用泛型方法打印不同字符串的元素：
 ![](/img/generic/method-1.png)
编译以上代码，运行结果如下所示：
>整型数组元素为:1 2 3 4 5 <br/>
双精度型数组元素为:1.1 2.2 3.3 4.4 <br/>
字符型数组元素为:<br/>
H E L L O

有界的类型参数:
可能有时候，你会想限制那些被允许传递到一个类型参数的类型种类范围。例如，一个操作数字的方法可能只希望接受Number或者Number子类的实例。这就是有界类型参数的目的。
要声明一个有界的类型参数，首先列出类型参数的名称，后跟extends关键字，最后紧跟它的上界。
下面的例子演示了"extends"如何使用在一般意义上的意思"extends"（类）或者"implements"（接口）。该例子中的泛型方法返回三个可比较对象的最大值。
 ![](/img/generic/method-2.png)
 
编译以上代码，运行结果如下所示：
>3, 4 和 5 中最大的数为 5<br/>
6.6, 8.8 和 7.7 中最大的数为 8.8<br/>
pear, apple 和 orange 中最大的数为 pear<br/>


## 总结
 1. 泛型的使用使我们的代码更加具有通用性，不会导致定义了一种类型之后其他的类型都无法使用该代码。
 2. 通过泛型可以定义类型安全的数据结构（类型安全），而无须使用实际的数据类型（可扩展）。这能够显著提高性能并得到更高质量的代码（高性能），因为您可以重用数据处理算法，而无须复制类型特定的代码（可重用）。
 
