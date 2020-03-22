## 一、抽象思想

> 所有编程语言都提供抽象机制

**人们通过计算机所能解决的问题的复杂性取决于抽象的类型质量。** 这里的类型是指抽象的是什么？

汇编语言是对底层机器的轻微抽象；

命令式语言是对汇编语言的抽象；

上面这两种语言所抽象的内容基于计算机的结构，而不是基于所要解决的问题的结构来考虑。

> 面向对象思想的实质是：程序可以通过新类型的对象使自身适用于某个特定的问题。

就是说，编写的代码一方面是对问题的解决，另一方面也是对问题的描述。所以，面向对象允许根据
问题来描述问题，而不是根据运行解决方案的计算机来描述问题。

理解面向对象可以把这个对象看作一台微型计算机--这台计算机具有状态、具有操作，用户可以根据这些
对象执行对应的操作

```
Alan Key曾经总结了第一个成功的面向对象语言，

同时也是Java所基于的语言之一的Smalltalk的五个基本特性，这个特性表现了一种纯碎的面向对象程序设计方式：

**1）万物皆对象**

**2）程序是对象的集合，它们通过发送消息来告知彼此所要做的**

**3）每个对象都有自己的由其他对象所构成的存储。** 换句话说，可以通过创建包含现有对象包的方式来创建新类型
的对象。因此，可以在程序中构建复杂的的体系，同时将其复杂性隐藏在对象的简单性的背后

**4）每个对象都拥有其类型也就是类，每个class，类和类型相同**

**5）某一特定类型的所有对象都可以接收同样的消息，体现了继承的思想**

```

------

Booach提出了一个更加简洁的描述：对象具有状态、行为和标识

## 二、创建对象和方法

> 每个类属于一种类型，通过关键字class来创建类，引入新的类型，通过类来创建对象，每个对象拥有类的属性和方法，并且每个对象都是唯一的

### 2.1 创建类

```java
/**
* 1、创建一个名为Light的类
* 通过class关键字，后面紧跟着的是class的名称
* 类名的首字母必须大写
*/
public class Light {
    // 代码块...
}
```

### 2.2 用引用操作对象

> **Java 一切都是对象，但我们操作的标识符实际上是对象的一个引用**
>
> 举个例子去理解，我们可以把对象和引用的关系想像成遥控器和电视机，遥控器就是引用，电视机就是对象
> 只要握住了这个遥控器，就能保持与电视机的链接，当我们想改变频道或者减少音量时，实际操作的是遥控器
> 再由遥控器来控制电视机。此外，即使没有电视机，遥控器也可以独立存在
>
> 也就是说，可以拥有引用，并不一定需要有一个对象与它关联

![](https://upload-images.jianshu.io/upload_images/2765653-4cc1f87fa296a08d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如果我们想操作 Light ，可以创建一个Light的引用：`Light light`

通过这种方式创建的只是引用宾不是对象。如果调用Light的方法，会返回一个运行时操作，因为此时light
并没有与任何事物相关联，因此，一种安全的做法是：创建一个引用同时便初始化

`Light light = new Light();`

> 创建对象必须采用new 
>
> 如果是字符串的话有两种方式：  
> 可以用带引号的文本初始化 `String s = "asdf"`   
> 也可以String s = new String("asdf");  

```java
/**
* 创建类的对象
*/
public class Test{
    /**
    * 1、创建Light类的对象且名称为：light
    */
    public static void main(String[] args){
        Light light = new Light();
        // 2、调用这个对象的方法
        // 用引用来操纵对象
        light.on(); 
        light.off();
    }
}
```


### 2.3 创建方法

> Java的方法决定了一个对象能够接收什么样的消息。
>
> 方法的基本组成部分包括：方法名、参数列表、返回值和方法体
> `ReturnType methodName(/* Argument list */){
      /*Method body*/
    }` 
> 
> 返回类型：描述的是在调用方法之后从方法返回的值
> 
> 参数列表：给出了要传给方法的信息的类型和名称
> 
> 方法名和参数列表，合起来被成为“方法签名”唯一地标识出某个方法
>
> Java中的方法只能作为类的一部分来创建，方法只有通过对象才能被调用


Java中的方法只能作为类的一部分来创建，方法只有通过对象才能被调用。且这个对象必须能执行这个方法调用。如果
试图在某个对象上调用它并不具备的方法，那么在编译时就会得到一条错误信息


```java
public class Light {
    // 代码块...
    /**
    * 2、给Light类添加方法：如打开、关闭
    */
    public void on(){
        // 代码块
    }
    // 没有返回值的方法
    // 使用void
    public void off(String s1,String s2,String s3){
            // 代码块
    }
}
```

### 2.4 调用带有参数列表方法

方法的参数列表指定要传递给方法什么样的消息。参数列表中必须指定每个传递对象类型及名字，像
Java这种任何传递对象的场合一样，这里传递的实际上也是引用，并且引用的类型必须正确。如果
参数被设为String类型，则必须传递一个String对象；否则，编译器会报错

```java

public class Test{
    public static void main(String[] args){ 
        Light light = new Light();
        String s1 = "aa";
        String s2 = "bb";
        String s2 = "cc";
        // 对象调用带有参数列表的方法
        light.off(s1,s2,s3);
        
    }
}
```

### 2.5 调用带有返回值的方法

> return关键字，包含两方面：首先表示"已经处理完，离开当前方法"。其次，如果此方法产生了
一个值，这个值要放在return关键字后面。 
> 
> 如果返回类型是void，return关键字的作用只是用来退出方法，并且没有必要到方法结束时才离开
>，可以在任何地方返回


```java

public class Light {
    // 代码块...
    /**
    * 2、给Light类添加方法：如打开、关闭
    */
    public void on(){
        // 代码块
    }
    // 没有返回值的方法
    // 使用void
    public void off(String s1,String s2,String s3){
            // 代码块
    }
    // 有返回值的方法
    // 使用返回类型，数据类型或引用类型
    public int time(){
        // 代码块
    }
}

public class Test{
    public static void main(String[] args){ 
        Light light = new Light();
        // 返回值的类型必须与x的类型兼容
        int x = light.time();
        light.off(s1,s2,s3);
        
    }
}
```

### 2.6 给类增加字段

> 字段（也可以称为数据成员或成员变量）
> 
> 字段可以是基本类型也可以引用数据类型，如果是引用数据类型必须初始化该引用
>
> 每个对象都有用来存储其字段的空间且不能在对象间共享

```java
/**
* 类型 变量名 = 属性值；
*/
public class Light {
    /**
    * 定义了一个int类型的变量i
    * 且属性值为10
    */
    int i = 10;
    public static void main(String[] args){
        Light light = new Light();
        // 给字段赋值
        // 通过引用对象的成员
        light.i = 47;
    }
}
```

还有一种情况

```java
/**
* 要修改的数据位于当前对象包含的其他对象中
* 这种情况下，只需要再使用连接句点就可以
*/
public class Test{
    Light light = new Light();
    public static void main(String[] args){
        Test test = new Test();
        test.light.i = 50;   
    }

}
```

### 2.7 基本成员默认值

> 若类的某个成员是基本数据类型，即使没有进行初始化，Java也会确保它获取一个默认值，
> 只有当变量作为类的成员使用时，Java才确保给定其默认值，
> 以确保哪些是基本类型的成员变量得到初始化，防止产生程序错误。
> 如果是局部变量，Java不会给默认值，如果在初始化时没有赋值，编译时会报错


### 2.8 static关键字

> 当声明一个方法或变量为使用static关键字时，就意味着这个域或方法不会与包含它的那个类的任何对象实例关联在一起。
> 所以，即使没有创建某个类的任何对象，也可以调用其static方法或访问其static域

```java
class StaticTest{
    static int i = 47;
    static void test(){
        // 代码块
    }
    public static void main(String[] args){
        //  一种方式，不需要创建类的对象，直接访问
        int a = StaticTest.i;
        // 另一种方式，可以创建类的对象，然后通过引用去访问
        // 需要注意的是，就算创建多个对象，所有对象都共享同一个i
        StaticTest staticTest1 = new StaticTest();
        StaticTest staticTest2 = new StaticTest();
        int b = staticTest1.i;
        int c = staticTest1.i;
    }
}
```

### 2.9 构件一个Java 程序

> 构件一个Java程序，会包含几个部分：
> 
> 定义包名：为了给一个类库生成不会与其他名字混淆的名字，Java包名采用反转域名来定义，
> 整个包名使用小写，句点用来代表子目录的划分：`com.packagename.utility`
>
> 使用其他类库：import指示编译器导入一个包，也就是一个类库：`import java.util.ArrayList`
> 这行代码告诉编译器，想要使用Java的ArrayList类。
> 并且可以使用通配符"*" 来省略，从而使用util中所有的类 `import java.util.*`

#### 一个完整的程序

```java
package com.packagename.utility;
public class ShowProperties{
    public static void main(String[] args){
        System.out.println("Hello World");
    }
}
```
#### 程序的编译与运行

> 要编译、运行这个程序，首先必须要有一个Java开发环境。安装好的JDK后需要设置classpath，以确保
> 计算机能找到javac和java这两个文件
> 
> 以上都准备好，将上面完整的程序保存到一个.java为结尾的文件中，并在命令行执行 `javac filename.java`
>
> 正常情况下，这行命令不会产生任何响应。然后在命令行继续输入 `java filename`
>
> 这之后就可以看到 "Hello World" 输出

![](https://upload-images.jianshu.io/upload_images/2765653-e73b5bf7d9176f00.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


#### JVM、JRE、JDK三者之间的关系

> Java通过JVM虚拟机与平台交互，JRE包含JVM
> 
> JVM就是一个虚拟的用于执行bytecode字节码的 "虚拟计算机"
>
> JRE包含：Java虚拟机、库函数、运行Java应用程序所必须的文件。运行一个JAVA程序
>
> JDK：包含JRE，以及增加编译器和调试器等用于程序开发的文件。开发Java程序

### 包

> 包内包含一组类，它们在单一的名字空间之下被组织在了一起。
  
假如我们要使用java.util包中的ArrayList类，有两种方式：

```java
// 一种方式：用其全名java.util.ArrayList来指定
public class FullQualification{
    public static void main(String[] args){
        java.util.ArrayList list = new java.util.ArrayList();
    }
}
``` 

```java
// 另一种方式：使用import关键字
// 如果想导入单一的类，可以在imoport语句中命名该类，但是在java.util中的其他类仍旧是不可用的
// 要想导入其中所有的类，只需要使用import java.util.*
import  java.util.ArrayList;
public class FullQualification{
    public static void main(String[] args){
        ArrayList list = new ArrayList();
    }
}
```

之所以要导入，就是要提供一个管理名字空间的机制。所有类成员的名称都是彼此隔离的。A类中的方法f()与B类中具有相同特征标记（参数列表）的方法f()不会彼此冲突。而类名称防止冲突，是通过Java对名称空间的完全控制并为每个类创建唯一标识符组合。

当编写一个Java源代码文件时，此文件通常被称为编译单元。每个编译单元都必须有一个后缀名.java，而在编译单元内则可以有一个public类，该类的名称必须与文件的名称相同(包括大小写，但不包括文件的后缀名.java)。每个编译单元只能有一个public类，否则编译器就不会接受。如果在编译单元之中还有额外的类的化，那么在包之外的世界是无法看见这些类的，这是因为它们不是public类，而且它们主要用来为主public类提供支持

当编译一个.java文件时，在.java文件中的每个类都会有一个输出文件，而该输出文件的名称与.java文件中每个类名相同，只是后缀为.class。因此，在编译少量.java文件之后，就得到大量的.class文件。

> 类库实际上是一组类文件。其中每个文件都有一个public类，以及任意数量的非public类。因此每个文件都有一个构件，如果希望这些构件(每个都有它们自己的独立的.java和.class文件)从属于同一个群组，就可以使用关键字packge

如果使用packge语句，它必须是文件中除注释以外的第一句代码。在文件的起始处写：

```
packge access;
```

就表示你在声明该编译单元是为access的类库的一部分。或者，你正在声明的编译单元中的public类名称是位于access名称下。任何想使用该编译单元的人必须指定全名或者与access结合使用关键字import(要注意的是，Java包的命名规则全部使用小写字母，包括中间的字也是如此)

```java
// 在access.mypackage 定义类MyClass
package access.mypackage;
public class MyClass{}

// 使用MyClass类
// 第一种方式：全名
public class QualifiedMyClass{
    public static void main(String[] args){
        access.mypackage.MyClass m = new access.mypackage.MyClass();
    }
}

// 第二种方式：import
import access.mypackage.*;

public class QualifiedMyClass{
    public static void main(String[] args){
        MyClass m = new MyClass();
    }
}
```

### 创建独一无二的包名

包可以由许多.class文件构成。怎样创建独一无二的名称以及怎样查找有可能隐藏于目录中某处的类。这是通过将.class文件所在的路径位置编码成package的名称来实现的。按照管理，package名称的第一部分是类的创建者的反顺序的Internet域名，第二部分是把package名称分解为你机器上的一个目录。所以当Java程序运行并且需要加载.class文件的时候，它就可以确定.class文件在目录上所处的位置


### 冲突

如果将两个含有相同名称的类库以 * 的形式同时导入？

```
import new.mindview.simple.*;
import java.util.*;
```
由于java.util.*也含有一个Vector类，这就存在潜在的冲突。如果现在要创建一个Vector类的化，就会产生冲突：

```
Vector v = new Vector(); 
```
这将产生一个问题，编译器并不清楚要用哪个Vector，此时编译器会要求你明确指明。

```
java.util.Vector v = new java.util.Vector(); 
```

## 三、理解对象

> 我们介绍如何创建类和对象。类提供了一个模版，然后基于类的模版创建不同的对象。
> 
> 当我们在开发或理解一个程序设计时，最好的方法之一就是将对象想象为"服务的提供者"，
> 对于用户来说，程序本身就是向用户提供服务，对于程序来说，它是通过调用不同的对象提供的服务来
> 实现这一目的的
>
> 所以我们的目标就是去创建（或者在现有代码库中寻找）能够提供理想的服务来解决问题的一些列的对象
>
> 这样做好处是：有助于提高对象的内聚性，高内聚是软件设计的基本质量要求之一：这意味着一个软件构件
> 的各个方面组合得很好，在高内聚代码中使用不同的对象完成不同的功能，最终将这些功能组合在一起

## 四、操作符

> 在最底层，java中的数据是通过使用操作符来操作的
> 
> 1）操作符用于操作数，生成一个新值
> 
> 2）有些操作符可能会改变操作数自身的值，这被称为 "副作用"，如++ --

### 4.1 算术运算符

假设整数变量a的值为10，变量b的值为20，遍历变量C是A和B经过操作符运算后的值

|  操作符 | 名称| 描述| 举例  |
|  ----  | ----  |----  |----  |
| +  | 加法 |相加运算符两侧的值 | int c = a + b; //c：30|
| -  | 减法 |左操作数减去右操作数 |int c = a - b; //c：-10 |
|* |  乘法|相乘操作符两侧的值 |int c = a * b;  //c：200 |
| /|除法  | 左操作数除以右操作数| int c = a / b;  //c：2|
| %| 取余 | 左操作数除以右操作数的余数| int c = a % b;  //c：0|
| ++|  自增| 操作数的值增加1|b++;或++b; // b:21 |
|-- | 自减 | 操作数的值减少1|b--;或--b; // b=19 |

### 4.2 优先级 

当一个表达式中存在多个操作符时，操作符的优先级就决定了各部分的计算顺序。Java对计算顺序做了特别的规定。其中，最简单的规则就是先乘除后加减。因为有时会忘记其他优先级规则，所以应该用括号明确规定规定计算顺序

### 4.3 字符串连接符

当一个String后面紧跟着一个+，而这个+的后面又紧跟一个非String类型的元素时，就会尝试着将这个非String类型的元素转换为String

```java
public class Precedence{
    public static void main(String[] args){
        System.out.println("abc" + 1);
    }
}
```

### 4.4 赋值运算符

> - 赋值使用操作符 "=" 。它的含义是：将等号右边的值赋值给等号左边的值
> 
> - 右边的值可以是任何常数、变量或者表达式（表达式只要它能生成一个值就行）
>
> - 左边的值必须是一个明确的，已命名的变量。这句话是说我们在声明一个变量的变量，必须声明变量的类型
> ，比如`int i` ,int就是变量的类型
>
> - *基本数据类型存储了实际的数值，而非指向一个对象的引用，所以在为其复制的时候，是直接将一个地方的内容
>复制了另一个地方。对基本数据类型使用a=b，那么b的内容就复制给a。若接着又修改了a，此时b根本不会受这种修改的影响
>
> - *但对象赋值的时候，要记住的是我们在对一个对象进行操作时，我们真正操作的是对对象的引用。
> 假使将一个对象赋值给另一个对象，实际是将引用从一个地方复制到另一个地方。这意味着假使对象使用c=d，那么c和d都指向的
> 是原本只有d指向的那个对象，此时我们通过b或c来修改原来的对象，b和c调用那个对象返回的值都是最新的。

```java
class tank{
    int level;
}

public class Assignment{
     public static void main(String[] args){
        Tank t1 = new Tank();
        Tank t2 = new Tank();
        t1.level = 9;
        t2.level = 47;
        System.out.println("1 : t1.level: " + t1.level + ", t2.level: " + t2.level);
        t1 = t2;
        System.out.println("2 : t1.level: " + t1.level + ", t2.level: " + t2.level);
        t1.level = 27;
        System.out.println("3 : t1.level: " + t1.level + ", t2.level: " + t2.level);
  }
}
// Output
// 1: t1.level: 9,t2.level: 47
// 2: t1.level: 47,t2.level: 47
// 3: t1.level: 27,t2.level: 27
```

分析：Tank类非常简单，它的两个实例（t1和t2）是在main()方法里创建。对每个Tank类对象都level域
都赋予了一个不同的值，然后将t2复制赋值给了t1，由于赋值操作的是一个对象的引用，所以修改t1的同时也改变了t2。
这就是因为t1和t2包含的都是相同的引用，他们指向相同的对象。

原本t1包含的对象的引用，是指向一个值为9的对象。在t1赋值的时候，这个引用被覆盖，也就是丢失了；
而那个不再被引用的对象会由"垃圾回收器"自动清理了

这种特殊的现象通常称作"别名现象"，是Java操作对象的一种基本方式。在上面的例子中，如果想避免别名问题应该怎么办呢？可以这些写：

```
t1.level = t2.level;
```

这样便可以保持两个对象彼此独立，而不是将t1和t2绑定相同的对象。但直接操作对象内的域容易导致混乱，并且
违背了良好的面向对象程序设计的原则。

### 4.5 方法调用中的别名问题

将一个对象传递给方法时，也会产生别名问题：

```java
// f()传递只是x的引用，所以可以f()之外的对象
class Letter{
  char c;
}

public class PassObject{
    static void f(Letter y){
        y.c = 'z';
  }
    public static void main(String[] args){
        Letter x = new Letter();
        x.c = 'a';
        System.out.println("1: x.c: " + x.c);
        f(x);
        System.out.println("2: x.c: " + x.c);
  }
}

// Output:
// 1: x.c: a;
// 2: x.c: z;
```

### 4.6 一元加、减操作符

一元减号用于转变数据的符号而一元加号(+)只是为了与一元减号(-)相对应，但是它位于的作用仅仅是将较小类型的操作数提升为int（（byte，short，char转型为int）

```
x = a * -b; // 编译器能正确识别
x = a * (-b) // 比较明确的写法
```

### 4.7 自动递增和递减

> 递增操作符是--，递减操作符++；
> 这两个操作符各有两种使用方式，通常称为 前缀式和后缀式

前缀递增表示++操作符位于变量或表达式的前面，--操作符类似
后缀递增表示++操作符位于变量或表达式的后面，--操作符类似

对于前缀递增和前缀递减(++a或--a)，表示会先执行运算，在生成值
对于后缀递增和后缀递减(a++或a--)，会先生成值，在执行运算

```
public class AutoInc{
    public static void main(String[] args){
        int i  = 1;
        System.out.println("i : " + i);
        System.out.println("i : " + ++i);
        System.out.println("i++ : " + i++);
        System.out.println("i: " + i);
        System.out.println("--i: " + --i);
        System.out.println("i-- : " + i--);
        System.out.println("i: " + i);
    }
}

// Output:
i : 1
++i : 2
i ++ : 2
i : 3
--i : 2
i-- : 2
i : 1
```

### 4.8 关系操作符

> 关系操作符生成的是一个boolean(布尔)结果，它们计算的是操作数的值之间的关系。如果关系是真实的，关系表达式会生成true；如果关系不真实，则生成false。
>  
> 关系操作符包括小于(<)、大于(>)、小于等于(<=)、大于等于(>=)、等于(==)、不等于(!=)；
  

== 和 != 适用于所有的基本数据类型，而其他比较符不适用于boolean类型。因为boolean值只能为true或false，大于和小于没有实际意义
  
== 和 != 比较基本类型的是值，也适用于所有对象，比较的就是对象的引用
                                               
### 4.9 equals()

> 用来比较两个对象的实际内容是否相同，但这个方法不适用于“基本类型”，基本类型直接使用== 和!=即可

```java
public class EqualMethod{
    public static void main(String[] args){
        Integer n1 = new Integer(47);
        Integer n2 = new Integer(47);
        System.out.println(n1.equals(n2));
    }
}

// Output
// true
```

### 4.10 逻辑操作符

> 逻辑运算符 与(&&)、或(||)、非(!)能根据参数的逻辑关系，生成一个布尔值(true或false)
  
逻辑运算符操作只可应用于布尔值，不可将一个非布尔值当作布尔值在逻辑表达式中使用
  
如果在应该使用String值的地方使用了布尔值，布尔值会自动转换成适当的文本形式
  
可以将整数类型转换成除布尔值以外的其他任何基本数据类型

```
public class Bool{
    public static void main(String[] args){
        Random rand = new Random(47);
        int i = rand.nextInt(100);
        int j = rand.nextInt(100);
        System.out.println("i = " + i);
        System.out.println("j = " + j);
        System.out.println("i > j is  " + (i > j));
        System.out.println("i < j is " +  (i < j));
        System.out.println("i >= j is " +  (i >= j));
        System.out.println("i <= j is " +  (i <= j));
        System.out.println("i == j is " +  (i == j));
        System.out.println("i != j is " +  (i != j));
        System.out.println(" (i < 10) && (j < 10) is " +  (i < 10) && (j < 10) ;
        System.out.println(" (i < 10) || (j < 10) is " +  (i < 10) || (j < 10) ;
    }
}

// Output
i = 58
j = 55
i > j is true
i < j is false
i >= j is true
i <= j is false
i == j is false 
i != j is true
(i < 10) && (j < 10) is fasle
 (i < 10) || (j < 10) is fasle

```

### 4.10 短路

> 一旦能够明确无误地确定整个表达式的值，就不再计算表达式余下部分了

```java
public class ShortCircuit{
    static boolean test1(int val){
        System.out.println("test1(" + val + ")");
        System.out.println("result : " + (val < 1));
        return val < 1;
    }
     static boolean test2(int val){
        System.out.println("test2(" + val + ")");
        System.out.println("result : " + (val < 2));
        return val < 2;
    }

 static boolean test3(int val){
        System.out.println("test3(" + val + ")");
        System.out.println("result : " + (val < 3));
        return val < 3;
    }

    public static void main(String[] args){
        boolean b = test(0) && test2(2) && test3(2);
        System.out.println("expression is : " + b);
    }
}

// Output
// test1()结果是true，表达式计算会继续下去，test2()结果是false，这意味着整个表达式肯定为false，所以没必要继续计算剩余的表达式。“短路”一词的由来正源于此。事实上。如果所有的逻辑表达式都有一部分不必计算，那将获得潜在的性能提升
// test1(0)
// result:true
// test2(2) 
// result:false
// expression is false
```

### 4.11 三元操作符

> 三元操作符也称条件操作符，它比较特别的是有三个操作数；但它确实属于操作符的一种，因为它最终也会生成一个值。

```
// 如果boolean-exp(布尔表达式)的结果为true，就计算value0，而且这个计算结果也就是操作符最终产生的值。
// 如果boolean-exp的结果为false，就计算value1，同样，它的结果也就成为了操作符最终产生的值
boolean-exp? value0 : value1 
```
                                                    
## 四、介绍三个关键字：public、private、protected

Java通过三个关键字public、private、protected在类的内部设定边界。这些关键字决定了类的使用范围

这三个关键字可以标识在类、方法、属性的前面

1）public ： 对于任何人都是可用的

2）private ：除类型的创建者和类型的内部方法之外的任何人都不能访问

3）protected ：继承类可以访问

除了上面的三个关键字外还有一个包访问权限，当没有使用上面任何3个关键字，这个时候，类拥有的就是权限就是，只可以访问同一个包中
的其他类的成员。

### 接口和实现

访问权限的控制常被称为是具体实现的隐藏。把数据和方法包装进类中，以及具体实现的隐藏，常被通常称为封装，其结果是一个同时带有特征和行为的数据类型

出于两个很重要的原因，访问权限控制将权限的边界划在了数据类型的内部。第一个原因是要设定程序可使用和不可使用的界限。可以在结构中建立自己的内部机制。第二个原因是：将接口和具体实现进行分离。

### 类的访问权限

为了控制类某个类的访问权限，修饰词必须出现于关键字class之前。

类既不可以是private的，也不可以是protected。所有对于类的访问权限，仅有两个选择：包访问权限或public。如果不希望其他任何人对该类拥有访问权限，可以把所有的构造器都指定为private，从而阻止任何人创建该类的对象。但是有一个例外，就是你在该类的static成员内部可以创建。


## 五、组合的概念

最简单地复用某个类的方式就是直接使用该类的一个对象，另外一种就是将那个类的一个对象置于某个新的类中

> 新的类可以由任意数量、任意类型的其他对象以任意可以实现新的类中想要的功能的方式所组成。这个概念
> 称为"组合" ，组合经常被视为"has-a"（拥有）关系，就像我们常说的"汽车拥有引擎"一样
>
> 将某个类的一个对象置于某个新的类中，这个行为可以称为 "创建一个成员对象"，新类的成员对象通常被声明为
> priate，这使得可以在不干扰使用的情况下， 修改这些成员，也可以在运行时修改这些成员对象，以实现动态修改程序的行为。

```java
class WaterSource{
    private String s;
    WaterSource(){
        System.out.println("WaterSource");
        s = "Constructed";
    }

    public String toString(){
        return s;
    }

}

public class SprinklerSystem {
    private String valve1;
    private String valve2;
    private String valve3;
    private String valve4;

    private WaterSource source = new WaterSource(); // 在SprinklerSystem类中使用 WaterSource类的对象
    private int i;
    private float f;

    @Override
    public String toString() { // 每个非基本类型的对象都有一个toString()方法，当编译器需要一个String而只有1个对象时，这个方法回被调用
        return "SprinklerSystem{" +
                "valve1='" + valve1 + '\'' +
                ", valve2='" + valve2 + '\'' +
                ", valve3='" + valve3 + '\'' +
                ", valve4='" + valve4 + '\'' +
                ", source=" + source + // 这里需要WaterSource的对象source ，当程序执行到这里时，回调用WaterSource的toString()方法，将source转换成一个String
                ", i=" + i +
                ", f=" + f +
                '}';
    }

    public static void main(String[] args) {
        SprinklerSystem sprinklers = new SprinklerSystem();
        System.out.println(sprinklers);
    }
}
/** Output:
WaterSource
SprinklerSystem{valve1='null', valve2='null', valve3='null', valve4='null',source=Constructed, i=0, f=0.0}
*/
```

以上代码执行结果中 ：valve1='null', valve2='null', valve3='null', valve4='null',说明一个问题：类中域为基本类型时能够自动被初始化为零，但是对象引用会被初始化为null。如果想要初始化引用，可以在代码中的下列位置进行：

1）在定义对象的地方，这意味着它们总是能够在构造器被调用之前被初始化

2）在类的构造器中

3）在正要使用这些对象之前，这种方式称为惰性初始化。在生成对象不值得及不必要每次都生成对象的情况下，这种方式可以减少额外的负担

4）使用实例初始化

```java
class Soap{
    private String s;
    Soap(){
        System.out.println("Soap()");
        s = "Constructed";
    }

    @Override
    public String toString() {
        return s;
    }
}
public class Bath {
    private String //在定义处初始化
        s1 = "Happy",
        s2 = "Happy",
        s3,s4;
    private Soap castille;
    private int i;
    private float toy;
    public Bath(){ // 在类的构造器中初始化
        System.out.println("Inside Bath()");
        s3 = "Joy";
        toy = 3.14f;
        castille = new Soap();
    }

    { i =47;} //实例初始化
    public String toString(){
        if(s4 == null){ //惰性初始化
            s4 = "Joy";
        }

        return
                "s1 = " + s1 + "\n" +
                "s2 = " + s2 + "\n" +
                "s3 = " + s3 + "\n" +
                "s4 = " + s4 + "\n" +
                "i = " + i + "\n" +
                "toy = " + toy + "\n" +
                "castille = " + castille;
    }

    public static void main(String[] args) {
        Bath b = new Bath();
        System.out.println(b);
    }
}
```



## 六、继承

> 当我们继承现有类时，也就创建了新的类，这个类不仅包括了现有类的所有成员，
> 和方法（现有类中的private成员和方法不可访问）。
>
> 因为子类拥有和父类相同的类型，所以，所有发送给父类对象的消息同时也可以发送给子类对象

如果要的父类和子类产生差异，有两种方法：

1）直接在子类添加新方法，这些方法并不是父类接口的一部分

2）覆盖，直接在子类中创建该类的新定义即可 

在上面的两种方式中，直接在子类添加新方法，子类和父类的关系是is-like-a（像是一个）关系，
is-a（是一个）关系就是继承中只覆盖基类的方法，而不添加父类中没有的新方法，子类和父类是完全相同的类型。

```java
class Cleanser{ // Cleanser类中的所有方法都必须是public的。这是因为，如果没有加任何访问权限修饰词，那么成员默认的访问权限是包访问权限，它仅允许包内的成员。因此，在此包中，如果没有访问权限修饰词，任何人都可以使用这些方法。但是其他包中的类要从Cleanser中继承，则只能访问public成员，所以，为了继承，一般的规则是将所有的数据成员都指定为private，将所有的方法指定为public
    private String s = "Cleanser";
    public void append(String a){
        s += a; // 使用“+=” 操作符号将String链接成s，此操作符是被Java设计者重载用以处理String对象的操作符之一，另一个是“+”
    }

    public void dilute(){
        append("dilute()");
    }

    public void apply(){
        append(" apply()");
    }

    public void scrub(){
        append(" scrub()");
    }

    @Override
    public String toString() {
        return s;
    }
}

public class Detergent extends Cleanser{

    public void scrub(){ // 覆盖基类的scrub()方法
        append(" Detergent.scrub()");
        super.scrub(); // 调用基类的方法 ，Java用super关键字表示超类的意思，当前类就是从超类继承的。所以super.scrub()将调用基类版本的scrub()方法
    }

    public void foam(){ // 增加新的方法
        append(" foam()");
    }

    public static void main(String[] args) {
        Detergent x = new Detergent();
        x.dilute();
        x.apply();
        x.scrub();
        x.foam();
        System.out.println(x);
        System.out.println("Testing base class;");
    }
}
```

### 初始化父类

当创建一个子类的对象时，该对象包含了一个父类的子对象。这个子对象与用父类直接创建的对象是一样的。而且区别在于，后者来自于外部，而父类的子对象被包装在子类对象内部

因此，对父类子对象的正确初始化也是至关重要，而且也仅有一种方法来包中这一点：在构造器中调用父类构造器来执行初始化，而父类构造器具有执行父类初始化的能力。Java会自动在子类中构造器中插入对父类构造器的调用

```java
class Art{
    Art(){
        System.out.println("Art constructor");
    }
}

class Drawing extends Art{
    Drawing(){
        System.out.println("Drawing constructor");
    }
}

public class Cartoon extends Drawing{

    public Cartoon(){
        System.out.println("Cartoon constructor");
    }

    public static void main(String[] args) {
        Cartoon x = new Cartoon();
    }
}
/** 执行结果 : 通过结果会发现，构建过程是从父类“向外”扩散的，所以父类在子类构造器可以访问它之前，就已经完成了初始化了。即使不为Cartoon()创建构造器，编译器也会为你合成一个默认的构造器，该构造器将待用父类的构造器
Art constructor
Drawing constructor
Cartoon constructor
*/
```

### 带参数的构造器

> 如果没有默认的父类构造器，或者想调用一个带参数的父类构造器，就必须用关键字super显式地编写调用父类构造器的语句，并且配以适当的参数列表

```java
class Game{
    Game(int i){
        System.out.println("Game constructor");
    }
}

class BoardGame extends Game{
    BoardGame(int i){
        super(i);
        System.out.println("BoardGame constructor");
    }
}
public class Chess extends BoardGame{
    Chess(){
        super(11); // 必须要在子类中调用父类的带参数的构造器
        System.out.println("Chess constructor");
    }

    public static void main(String[] args) {
        Chess x = new Chess();
    }
}
```


最后，还要注意的是，当创建一个类时，总是在继承，因此，除了已明确指出要从其他类中继承，否则就是在隐式地从Java的标准
根类Object进行继承

### 继承中的重载机制

> 如果Java的父类拥有某个已被多次重载的方法名称，那么在子类中重新定义该方法名称并不会屏蔽其在父类中的任何版本。因此，无论在子类或者它的父类中对方法进行定义，重载机制都可以正常工作

```java
class Homer{
    char doh(char c){
        System.out.println("doh(char)");
        return 'd';
    }
    
    float doh(float f){
        System.out.println("doh(float)");
        return 1.0f;
    }
}

class Milhouse{}

class Bart extends Homer{
    void doh(Milhouse m){
        System.out.println("doh(Milhouse)");
    }
}
public class Hide {
    public static void main(String[] args) {
        Bart b = new Bart();
        b.doh(1);
        b.doh('x');
        b.doh(1.0f);
        b.doh(new Milhouse());
    }
}
```

从上述例子中，可以看到，虽然Bart引入了一个新的重载方法，但是Bart中Homer的所有重载方法都是可用的。使用与基类完全相同的特征签名及返回类型来覆盖具有相同名称的方法，是一件极其平常的事。

> JavaSE5新增加了@Override注解，它并不是关键字，但是可以把它当作关键字使用，当你想要覆盖某个方法时，可以选择添加这个注解，但不小心重载而并非覆盖了该方法时，编译器就会生成一条错误消息。

### 在组合与继承之间选择

组合技术通常用于想在新类中使用现有类的功能而非它的接口这种情形。即，在新类中嵌入某个对象，让其实现所需要的功能，但新类的用户看到的只是为新类所定义的接口，而非所嵌入对象的接口。为取得此效果，需要在新类中嵌入一个现有类的private对象

在继承的时候，使用某个现有类，并开发一个它的特殊版本。通常，这意味着你在使用一个通用类，并为了某种特殊需要而将其特殊化。通常用“is-a”(是一个)的关系是用继承来表达的，而“has-a”(又一个)的关系则用组合来表达的

### 向上转型

> 继承除了为新的类提供方法，还有重要的方面是用来表现子类和父类之间的关系。这种关系可以用“新类是现有类的一种类型”这句话加以概括。

```java
class Instrument{
    public void play(){}
    static void tune(Instrument i){
        i.play();
    }
}
public class Wind extends Instrument{
    public static void main(String[] args) {
        Wind flute = new Wind();
        Instrument.tune(flute);  // flute是 Instrument子类Wind的对象，tune()方法可以接受Instrument引用，这里将Wind对象传递给tune()，由于Java对类型的检查十分严格，这里Wind对象同样也是一种Instrument对象，在tune()中，程序代码可以对Instrument和它所有的子类起作用，这种将Wind引用转换为Instrument引用的动作，称之为向上转型
    }
}
```

flute是 Instrument子类Wind的对象，tune()方法可以接受Instrument引用，这里将Wind对象传递给tune()，由于Java对类型的检查十分严格，这里Wind对象同样也是一种Instrument对象，在tune()中，程序代码可以对Instrument和它所有的子类起作用，这种将Wind引用转换为Instrument引用的动作，称之为向上转型

> 为什么称为向上转型

传统的类继承图的绘制方法：将根置于页面的顶端，然后逐渐向下：

![Wind.java的继承图](https://upload-images.jianshu.io/upload_images/2765653-1447fc8b0b479fa6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

由子类转型成父类，在继承图上是向上移动的，因此一般称为向上转型。由于向上转型是从一个较专用类型向通用类型转换，所以总是很安全的。也就是说，子类就是父类的一个超集。子类可能比父类含有更多的方法，但它必须至少具有基类中所含有的方法。

## 代理

> 除了组合和继承，还有一种可以复用类就是使用代理，Java并没有提供对它的直接支持。这是继承与组合之间的中庸之道，因为我们将一个成员对象置于所要构造的类中（就像组合），但于此同时我们在新类中暴露了该成员对象的所有方法（就像继承）

```java
public class SpaceShipControls {
    void up(int velocity){}
    void down(int velocity){}
    void left(int velocity){}
    void right(int velocity){}
    void forward(int velocity){}
    void back(int velocity){}
    void turboBoost(){}
}
```

```java
public class SpaceShipDelegation {
    private String name;
    private SpaceShipControls controls = new SpaceShipControls();
    public SpaceShipDelegation(String name){
        this.name = name;
    }

    public void back(int velocity){
        controls.back(velocity);
    }

    public void dowm(int velocity){
        controls.down(velocity);
    }

    public void forward(int velocity){
        controls.forward(velocity);
    }

    public void left(int velocity){
        controls.left(velocity);
    }

    public void right(int velocity){
        controls.right(velocity);
    }

    public void turboBoost(){
        controls.turboBoost();
    }

    public void up(int velocity){
        controls.up(velocity);
    }

    public static void main(String[] args) {
        SpaceShipDelegation protector = new SpaceShipDelegation("NSEA Protector");
    }
}
```

## final关键字

> final会使用到的三种情况：数据、方法和类
>
> final数据：
>
> 1）一个永不改变的编译时常量
> 
> 2）一个在运行时被初始化的值，而你不希望它被改变
>
> 对于编译期常量这种情况，在Java中，这类常量必须是基本数据类型，以关键字final修饰。在对这个常量进行定义的时候，必须对其进行赋值。
>
> 一个既是static又是final的域只占据一段不能改变的存储空间，用大写表示，并使用下划线分隔各个单词

当是对象引用而不是基本类型时，对于基本类型，final 使数值恒定不变；

对于对象引用，final使引用恒定不变。一旦引用被初始化指向一个对象，就无法再把它改为指向另一个对象。但对象自身是可以被修改的。Java并未提供任何使对象恒定不变的途径。

这样的限制同样适用数组，它也是对象

```java
class Value{
    int i;
    public Value(int i){
        this.i = i;
    }
}
public class FinalDate {
    private static Random rand = new Random(47);
    private String id;
    public FinalDate(String id){
        this.id = id;
    }

    private final int valueOne = 9; // 编译时常量
    private static final int VALUE_TWO = 99; // 公共常量

    public static final int VALUE_THREE = 39; // 公共常量

    private final int i4 = rand.nextInt(20); // 不能是编译时常量

    static final int INT_5 = rand.nextInt(20); // 不能是编译时常量

    private Value v1 = new Value(11);

    private final Value v2 = new Value(22); // final修饰对象

    private static final Value VAL_3 = new Value(33); // static final修饰对象

    private final int[] a = {1,2,3,4,5,6}; //final修饰数组

    public String toString(){
        return id + ": " + "i4 = " + i4 + ", INT_5 = " + INT_5;
    }

    public static void main(String[] args) {
        FinalDate fd1 = new FinalDate("fd1");
       // fd1.valueOne++; // 不能修改值，因为final修饰
        fd1.v2.i++; // 可以修改对象自身的值
        fd1.v1 = new Value(9); // 不是final指定的
        for(int i = 0; i < fd1.a.length;i++){
            fd1.a[i]++; // 可以修改数组内部的值
        }

       //fd1.v2 == new Value(0); // 不能给v2重新赋值新的对象
        //fd1.VAL_3 = new Value(1); // 不能重新赋值
        //fd1.a = new int[3]; // 不能重新赋值

        System.out.println(fd1);
        System.out.println("Creating new FinalDate");
        FinalDate fd2 = new FinalDate("fd2");
        System.out.println(fd1);
        System.out.println(fd2);
    }
}
```

valueOne和VAL_TWO 都是带有编译时数值的final基本类型，可以用作编译期常量
VAL_THREE 是一种更加典型的对常量进行定义的方式：定义为public，则可以被用于包之外；定义为static，则强调只有一份；定义为fianl，则说明它是一个常量。
i4和INT_5说明了不能因为某数据是final的就认为在编译时可以知道它的值。i4和INT_5也展示了final数值定义为静态和非静态的区别，在fd1和fd2中，i4的值是唯一的并且每次创建对象初始化的值是不同的，但INT_5的值是不可以通过创建第二个FinalData对象而加以改变的，此区别只有当数值在运行时内被初始化时才会显现。
v1、v2、VAL_3 说明了final引用的意义。由于v2是final的，就认为无法改变它的值。由于它是一个引用，final意味着无法将v2再次指向另一个新的对象。这对数组具有同样的意义，数组只不过是另一种引用。

### 空白final

Java允许生成“空白final”，所谓空白final是指被声明为final但又没有给定初值的域。必须在域的定义处或者每个构造器中用表达式对final进行赋值

```java
class Poppet{
    private int i;
    Poppet(int i){
        this.i = i;
    }
}
public class BlankFinal {
    private final int i = 0;
    private final int j;
    private final Poppet p;
    public BlankFinal(){
        j = 1;
        p = new Poppet(1);
    }
    
    public BlankFinal(int x){
        j = x;
        p = new Poppet(x);
    }

    public static void main(String[] args) {
        new BlankFinal();
        new BlankFinal(47);
    }
}
```

### final参数

Java允许在参数列表中以声明的方式将参数指明为final。这意味着你无法在方法中更改参数引用所指向的对象：

```java
class Gizmo{
    public void spin(){}
}
public class FinalArguments {
    void with(final Gizmo g){
       //  g = new Gizmo(); // 无法修改参数引用所指向的对象
    }
    void without(Gizmo g){
        g = new Gizmo();
        g.spin();
    }
    
    void f(final int i){ // 展示了当基本类型的参数被指明为final时所出现的结果：你可以读参数，但却无法修改参数。这一特性主要用来向匿名内部类传递数据
        //i++; // 不能修改
    }
    
    int g(final int i){
        return i + 1;
    }

    public static void main(String[] args) {
        FinalArguments bf = new FinalArguments();
        bf.without(null);
        bf.with(null);
        
    }
}
```

### final方法

类中所有的private方法都隐式地指定为是final的。由于无法取用private方法，所以也就无法覆盖它。可以对private方法添加final修饰词，但这并不能给该方法增加任何额外的意义

```java
class WithFinals{
    private final void f(){
        System.out.println("WithFinals.f()");
    }

    private void g(){
        System.out.println("WithFinals.g()");
    }
}

class OverridingPrivate extends WithFinals{
    private final void f(){
        System.out.println("OverridingPrivate.f()");
    }
    private void g(){
        System.out.println("OverridingPrivate.g()");
    }
}

class OverridingPrivate2 extends OverridingPrivate{
    public final void f(){
        System.out.println("OverridingPrivate2.f()");
    }

    public void g(){
        System.out.println("OverridingPrivate2.g()");
    }
}
public class FianlOverridingIllusion {
    public static void main(String[] args) {
        OverridingPrivate2 op2 = new OverridingPrivate2();
        op2.f();
        op2.g();

        OverridingPrivate op = op2;
        WithFinals wf = op2;
    }
}
```

覆盖只有在某方法是基类的接口的一部分时才会发现。即，必须能将一个对象向上转型为它的基本类型并调用相同的方法。如果某方法为private，它就不是父类接口的一部分，仅是一些隐藏于类中的程序代码，只不过是具有相同的名称而已。但如果在子类中以相同的名称生成一个public、protected或包访问权限方法的话，该方法就不会产生在父类中出现的“仅具有相同名称”的情况， 此时，并没有覆盖该方法，仅是生成了一个新的方法

### final类

> 当将某个类的整体定义为final时，就表明这个类不能被继承

```java
class SmallBrain{}

final class Dinosaur{
    int i = 7;
    int j = 1;
    SmallBrain x = new SmallBrain();
    void f(){}
}
public class Jurassic {
    public static void main(String[] args) {
        Dinosaur n = new Dinosaur();
        n.f();
        n.i = 40;
        n.j++;
    }
}
```

final域可以根据的个人的意愿选择是或不是final，不论类是否被定义为final，相同的规则都适用于定义为final域。然而，由于final类禁止继承，所以final了中所有的方法都隐式的指定为是final的，因为无法覆盖它们。在final类中可以给方法添加final修饰词，但这不会增加任何意义。

### 继承中的初始化及类的加载

在Java中的所有事物都是对象，每个类的编译代码都存在于它自己的独立的文件中。该文件只在需要使用程序代码时才会被加载。

一般来说，可以说"类的代码在除此使用时才会加载"，这通常是指加载发生于创建类的第一个对象时，但是当访问static域或static方法时，也会发生加载。

所有的staic对象和staic代码段都会在加载时依程序中的顺序（即，定义类时的书写顺序）而依次初始化。

```java
class Insect{
    private int i = 9;
    protected int j;
    Insect(){
        System.out.println("i = " + i + ", j = " + j);
        j = 39;
    }

    private static int x1 = printInit("static Insect.x1 initialized");
    static int printInit(String s){
        System.out.println(s);
        return 47;
    }
}
public class Bettle extends Insect{
    private int k = printInit("Beetle.k initialized");
    public Bettle(){
        System.out.println("k =  " + k);
        System.out.println("j =  " + j);
    }

    private static int x2 = printInit("static Beetle.x2 initialized");

    public static void main(String[] args) {
        System.out.println("Beetle constructor");
        Bettle b = new Bettle();
    }
}
/**
执行结果：
static Insect.x1 initialized // 父类的静态方法被调用，在创建对象前
static Beetle.x2 initialized // 子类的静态方法被调用，在创建对象前
Beetle constructor // main()方法开始执行
i = 9, j = 0 // 父类的构造器执行，在此之前，父类的字段初始化，没有赋值的基本类型被置为默认值，对象应用被设为 null，
Beetle.k initialized // 子类的字段初始化
k =  47 // 子类的构造器执行
j =  39
*/
```

在Bettle类上运行Java时，所发生的第一件事情就是访问Bettle.main()（一个static），于是加载器开始启动并找出Bettle类的编译代码
（在名为Bettle.class的文件之中）。在对它进行加载的过程中，编译器注意到它有一个父类（通过由关键字extends得知的），于是它继承进行加载。不管你是否
打算产生一个父类的对象，这都要发生。

如果该父类还有其自身的父类，那么第二个父类就会被加载，如此类推。接下来，根父类中的static初始化（Insect类）即会被执行，然后是下一个子类，以此类推。这种方式很重要，因此子类的static初始化可能会依赖于父类成员能否被正确初始化

至此为止所有的类都加载完毕，对象就可以创建了。首先，对象中所有的基本类型都会被设为默认值，对象
引用被设为null--这是通过将对象内存设为二进制而一句生成的。然后，父类的构造器会被调用。在生疏例子中，它是被自动调用的。
但也可以用super来指定对父类类构造器的调用。

## 多态

> 面向对象的程序设计语言的三大特征是：抽象、继承、多态
> 
> 封装通过合并特征和行为来创建新的数据类型。
> 
> 实现隐藏则通过将私有化把接口和实现分离。
>
> 多态的作用是消除类型之间的耦合关系。
>
> 继承允许将对象视为它自己本身的类型或其父类型来加以处理。
> 允许将多种类型（从同一父类继承的）视为同一类型来处理。
> 多态方法调用允许一种类型表现出与其他相似类型之间的区别，只要它们都是从同一父类继承而来的。
> 这种区别是根据方法行为的不同而表现出来的，虽然这些方法都可以通过同一父类来调用

### 再论向上转型

> 对象既可以作为它自己本身的类型使用，也可以作为它的父类型使用。而这种把某个对象的引用视为对其父类型的引用的做法被称作向上转型

```java
class Instrument{
    public void play(Note n){
        System.out.println("Instrument.play()");
    }
}
public class Wind extends Instrument{
    public void play(Note n){
        System.out.println("Wind.play() " + n);
    }
}
```

```java
public class Music {
    public static void tune(Instrument i){ // 接受一个Instrument 引用，同时也接受任何Instrument的子类
        i.play(Note.MIDDLE_C);
    }

    public static void main(String[] args) {
        Wind flute  = new Wind();
        tune(flute);
    }
}
```

```java
public enum Note {
    MIDDLE_C,C_SHARP,B_FLAT;
}
```

### 方法调用绑定

将一个方法调用和一个方法主体关联起来被称作绑定。在上面的代码中，因为编译器只有1个Instrument引用时，它无法知道究竟调用哪个方法，解决的方法就是后期绑定，后期绑定的含义就是在运行时根据对象的类型进行绑定。后期绑定也叫做动态绑定或运行时绑定。也就是说，编译器一直不知道对象的类型，但是方法调用机制能找到正确的方法体，并加以调用。

Java中除了static方法和final方法(private方法属于final方法)之外，其他所有的方法都是后期绑定。这意味着通常情况下，我们不必判断是否应该进行后期绑定--它会自动发生

为什么要将某个方法声明为final呢？它可以防止其他人覆盖该方法。最重要的一点是：这样可以有效地关闭动态绑定。或者说，告诉编译器不需要对其进行动态绑定。这样，编译器就可以为final方法调用生成更有效的代码

一旦直到Java中所有方法都是通过动态绑定实现多态后，就可以编写只与父类打交道的程序代码了，并且这些代码对所有的子类都可以正确运行。或者说，发送消息给某个对象，让该对象去断定应该做什么事

![继承图](https://upload-images.jianshu.io/upload_images/2765653-65e84649cfcdd5bd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> 向上转型可以像下面这条语句这么简单：```Shape s = new Circle();```

此时调用父类方法（父类方法已经在子类中被覆盖）：```s.draw();```，由于后期绑定（多态），还是正确调用了```Circle.draw()```方法

![](https://upload-images.jianshu.io/upload_images/2765653-e970269bf2686a48.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```java
package com.testya.test;

class Instrument{
    void play(Note n){
        System.out.println("Instrument.play() " + n);
    }
    String what(){
        return "Instrument";
    }

    void adjust(){
        System.out.println("adjusting instrument");
    }
}

class Wind extends Instrument{
    void play(Note n){
        System.out.println("Wind.play() " + n);
    }
    String what(){
        return "Wind";
    }

    void adjust(){
        System.out.println("adjusting Wind");
    }
}

class Percussion extends Instrument{
    void play(Note n){
        System.out.println("Percussion.play() " + n);
    }
    String what(){
        return "Percussion";
    }

    void adjust(){
        System.out.println("adjusting Percussion");
    }
}

class Stringed extends Instrument{
    void play(Note n){
        System.out.println("Stringed.play() " + n);
    }
    String what(){
        return "Stringed";
    }

    void adjust(){
        System.out.println("adjusting Stringed");
    }
}

class Brass extends Wind{
    void play(Note n){
        System.out.println("Brass.play() " + n);
    }
    void adjust(){
        System.out.println("adjusting Brass");
    }
}

class Woodwind extends Wind{
    void play(Note n){
        System.out.println("Woodwind.play() " + n);
    }
    void adjust(){
        System.out.println("adjusting Woodwind");
    }
}
public class Music3 {
    public static void tune(Instrument i){
        i.play(Note.MIDDLE_C);
    }

    public static void tuneAll(Instrument[] e){
        for(Instrument i : e){
            tune(i);
        }
    }

    public static void main(String[] args) {
        Instrument[] Orchestra = {new Wind(),new Percussion(),new Stringed(),new Brass(),new Woodwind()};
        tuneAll(Orchestra);
    }
}
```

```java
public enum Note {
    MIDDLE_C,C_SHARP,B_FLAT;
}
```

### 域和静态方法
    
```java
class Super{
    public int field = 0;
    public int getField(){
        return field;
    }
}

class Sub extends Super{
    public int field = 1;
    public int getField(){
        return field;
    }
    public int getSuperField(){
        return super.field;
    }
}
public class FieldAccess {
    public static void main(String[] args){
        Super sup = new Sub();
        System.out.println("sup.field = " + sup.field + " , sup.getField() = " + sup.getField());

        Sub sub = new Sub();
        System.out.println("sub.field = " + sub.field + " , sub.getField() = " + sub.getField() + " , sub.getSuperField() = " + sub.getSuperField());
    }
}
```

当Sub对象转型为Super引用时，任何域访问操作都将由编译器解析，因此不是多态的。在上面的例子中，为Super.field和Sub.field分配了不同的存储空间。这样，Sub实际上包含两个称为field的域：它自己的和它从Super处得到的。然而在引用Sub中的field时所产生默认域并非Super版本的field域。因此，为了得到Super.field，必须显式地指明super.field。在实际开发中，首先要将所有的域设置成private，因此不能直接访问它们，其副作用是只能调用方法来访问。另外，不要对父类中的域和子类中的域赋予相同的名字，因为这种做法容易令人混淆

如果某个方法是静态的，它的行为就不具有多态性：静态方法是与类，而并非与单个对象相关联的

```java
class StaticSuper{
    public static String  staticGet(){
        return "Base staticGet()";
    }

    public String dynamicGet(){
        return "Base dynamicGet";
    }
}

class StaticSub extends StaticSuper{
    public static String  staticGet(){
        return "Derived staticGet()";
    }

    public String dynamicGet(){
        return "Derived dynamicGet";
    }
}
public class StaticPolymorphism {
    public static void main(String[] args) {
        StaticSuper sup = new StaticSub();
        System.out.println(sup.staticGet());
        System.out.println(sup.dynamicGet());
    }
}
```

### 构造器和多态

构造器实际上是static方法，只不过该static声明是隐式的，所以构造器并不具有多态性

> 构造器在多态的层次结构中的调用顺序
  
子类构造过程中调用父类的构造器，而且是按照继承层次逐渐向上链接，以使每个父类的构造器都能得到调用。这样做的原因是：因为构造器的重要任务之一是：检查对象是否被正确地构造，子类只能访问它自己的成员，不能访问父类的成员（父类成员通常是private的）。所以只有父类才能正确的初始化。因此所有的构造器都必须得到调用。在子类的构造器中，如果没有明确指定调用某个父类构造器，子类构造器会自动调用默认构造器，如果不存默认构造器，编译器就会报错（若某个类没有构造器，便器会自动合成出一个默认构造器）

```java
class Meal{
    Meal(){
        System.out.println("Meal()");
    }
}

class Bread{
    Bread(){
        System.out.println("Bread()");
    }
}

class Cheese{
    Cheese(){
        System.out.println("Cheese()");
    }
}

class Lettuce{
    Lettuce(){
        System.out.println("Lettuce()");
    }
}

class Lunch extends Meal{
    Lunch(){
        System.out.println("Lunch()");
    }
}

class PortableLunch extends Lunch{
    PortableLunch(){
        System.out.println("PortableLunch()");
    }
}


public class Sandwich extends PortableLunch{
    private Bread b = new Bread();
    private Cheese c = new Cheese();
    private Lettuce l = new Lettuce();
    public Sandwich(){
        System.out.println("Sandwich()");
    }

    public static void main(String[] args) {
        new Sandwich();
    }
}
/** 执行结果：
Meal()
Lunch()
PortableLunch()
Bread()
Cheese()
Lettuce()
Sandwich()
*/
```

上面的例子中，每个类都有构造器，并且Sandwich体现了三层继承关系以及三个成员对象。当在main()方法里创建Sandwich()对象后，就可以看到输出结果：

1）先调用父类的构造器，这个步骤会不断的反复递归下去，首先是Meal类，然后是下一层子类Lunch，最后是PortableLunch

2）按声明顺序调用Sandwich成员的初始化方法

3）调用Sandwich构造器

### 构造器内部的多态方法

在一般的方法内部，动态绑定的调用是在运行时才决定的，因为对象无法知道方法所在的那个类，还是属于那个类的子类

如果要调用的构造器内部的一个动态绑定方法，就是用到那个方法的被覆盖后的定义，这个调用的效果可能相当难以预料，因此被覆盖的方法在对象被完全构造之前就会被调用。

```java
class Glyph{
    void draw(){
        System.out.println("Glyph.draw()");
    }

    Glyph(){
        System.out.println("Glyph() before draw()");
        draw();;
        System.out.println("Glyph() after draw()");
    }
}

class RoundGlyph extends Glyph{
    private int radius = 1;
    RoundGlyph(int r){
        radius = r;
        System.out.println("RoundGlyph.RoundGlyph(),radius = " + radius);
    }
    
    void draw(){
        System.out.println("RoundGlyph.draw(),radius = " + radius);
    }
}
public class PloyConstructors {

    public static void main(String[] args) {
        new RoundGlyph(5);
    }
}
```

在上面的例子中，Glyph.draw()方法设计为被覆盖，这种覆盖是在RoundGlyph发生的。但是Glyph构造器会调用这个方法，结果导致了对
RoundGlyph.draw()的调用。但是从输出结果看，此时radius不是默认初始值1，而是0

所以，初始化的实际过程是：

1）在其他任何事物发生之前，将分配给对象的存储空间初始化成二进制的零

2）如前所述那样调用父类的构造器。此时，调用被覆盖后的draw()方法（在RoundGlyph构造器之前调用），由于步骤1的缘故，此时发现radius的值为0

3）按照声明的顺序调用成员的初始化方法

4）调用子类的构造器主体

因此，编译构造器时有一条有效的准则：用尽可能简单的方法使对象进入正常状态；如果可以的话，避免调用其他方法。在构造器中唯一能够安全调用的那些方法是父类中的final方法（也适用于private方法，它们自动属于final方法，这些方法不能被覆盖）

### 协变返回类型

JavaSE5 中添加了协变返回类型，它表示在子类中的被覆盖的方法可以返回父类方法的返回类型的某种子类类型

```java
class Grain{
    public String toString(){
        return "Grain";
    }
}

class Wheat extends Grain{
    public String toString(){
        return "Wheat";
    }
}

class Mill{
    Grain process(){
        return new Grain();
    }
}

class WheatMill extends Mill{
    Wheat process(){
        return new Wheat();
    }
}
public class CovariantReturn {
    public static void main(String[] args) {
        Mill m = new Mill();
        Grain g = m.process();
        System.out.println(g);
        m = new WheatMill();
        g = m.process();
        System.out.println(g);
    }
}
```

### 用继承进行设计

```java
class Actor{
    public void act(){}
}

class HappyActor extends Actor{
    public void act(){
        System.out.println("HappyActor");
    }
}

class SadActor extends Actor{
    public void act(){
        System.out.println("SadActor");
    }
}

class Stage{
    private Actor actor = new HappyActor();
    public void change(){
        actor = new SadActor();
    }
    
    public void performPlay(){
        actor.act();
    }
}
public class Transmogrify {
    public static void main(String[] args) {
        Stage stage = new Stage();
        stage.performPlay();
        stage.change();
        stage.performPlay();
    }
}
```

在上面的例子中：Stage对象包含一个对Actor的引用，而Actor被初始化为
HappyActor对象。这意味着performPlay()会产生某种行为，并且SadActor对象的引用可以在actor中被替代，performPlay()产生的行为也随之改变。这样一来，我们在运行期间获得了动态灵活性（这也称作状态模式）

通常：用继承表达行为间的差异，用字段表达状态上的变化。在上述例子汇总，两者都用到了：通过继承得到了两个不同的类，用于表达act()方法的差异，而Stage通过运用组合使自己的状态发生变化。在这种情况下，状态的改变也就产生了行为的改变。

### 纯继承域扩展

用纯继承的方式创建继承层次结构，也就是说，只有在父类中已经建立的方法才可以在导出类中被覆盖。这种被称作是纯碎的is-a(是一种)关系，因为一个类的接口已经确定了它应该是什么。继承可以确保所有子类具有父类的接口，且绝对不会少。在使用中子类可以完全替代父类，而且使用子类时，完全不需要知道关于子类的任何额外信息，因为父类可以接受发送给子类的任何消息，由于二者有完全相同的接口，我们只需从子类向上转型，用于不需要正在处理的对象的确切类型。所有这一切，都是通过多态来处理的

但是在实际开发中，扩展接口才是解决特定问题的完美方案。这可以在称为“is-like-a”(像一个)关系，因为子类就像是一个父类-拥有父类相同的基本接口，但是子类还可以具有额外方法实现的其他特性

但这种方式也具有其缺点，就是子类的部分接口是不能被父类访问的，这时，一旦向上转型，就不能调用子类中父类中并没有定义的那些方法

### 向下转型与运行时类型识别

在Java中，所有的转型都会得到检查！所以即使我们只是进行一次普通的加括号形式的类型转换，在进入运行期时仍然会对其进行检查，以保证它的确是我们希望的哪种类型，否则，如果不是，就会返回一个ClassCastException（类转型异常），这种在运行期间对类型进行检查的行为称作“运行时类型识别”（RTTI）

```java
class Useful{
    public void f(){}
    public void g(){}
}

class MoreUseful extends Useful{
    public void f(){}
    public void g(){}
    public void u(){}
    public void v(){}
    public void w(){}
}
public class RTTI {
    public static void main(String[] args) {
        Useful[] x = {new Useful(),new MoreUseful()};
        x[0].f();
        x[0].g();
        ((MoreUseful)x[1]).u(); // RTTI 向下转型
        // ((MoreUseful)x[0]).u();  // ClassCastException ，Useful对象不能转型为MoreUseful
    }
}
```

## 七、后期绑定、向上转型的概念

> 在处理类型的层次结构时，经常把一个对象不当作它所属的特定类型的对象，而是将其当作其父类的对象。这就称为"泛化""
> 这样可以编写出不依赖特定类型的代码

使用泛化将会产生一个问题，但我们将子类当作父类来看待时，会存在一个问题，编译器在编译时是不可能知道
自己哪一段代码将被执行，那对象如何根据自身的具体类型来执行相应的代码呢？

在下面的图中，BirdController对象仅仅处理泛化的Bird对象，而不了解它们的确切类型。
从BirdController的角度看，这么做非常方便，因为不需要编写特别的代码来判定要处理的Bird对象的确切类型或其行为。
当move()方法被调用时，即便忽略Bird的具体类型，也会产生正确的行为（Goose（鹅）会走、非或游泳，Penguin（企鹅）走或游泳），

这是如何发生的呢？

![](https://upload-images.jianshu.io/upload_images/2765653-ffe0e926f8e5be21.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

所以为了解决这个问题，**面向对象程序设计语言使用了后期绑定的概念。**当向对象发送消息时，被调用
的代码直到运行时才能确定。编译器在编译时确保被调用方法的存在，并对调用参数和返回值执行类型检查，
但是并不直到将被执行的确切代码。

**为了执行后期绑定，Java使用了一段特殊的代码替代绝对地址调用。这段代码使用在对象存储的信息来计算方法体的地址。**
这样，根据这一小段代码的内容，每个对象都可以具有不同的行为表现，当向一个对象发送消息时，该对象就能知道对这条消息应该做些什么。
**在Java中，动态绑定是默认行为，不需要添加额外的关键字来实现多态**

> 向上转型：因为动态绑定，所以发送给父类的任何消息，子类都可以接收，那么将子类看作是它的父类的过程称为向上转型。

![](https://upload-images.jianshu.io/upload_images/2765653-5d1bce38758271cc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


```java
/**
* 编写方法，接收一个父类类型作为参数
**/
public class Test{
    void doSomething(Shape shape){
        shape.erase();
        shape.draw();
    }
    public static void main(String[] args){
      Circle circle = new Circle(); // 创建子类对象
      Triangle triangle = new Triangle(); 
      Line line = new Line();
      doSomthing(circle); // 调用doSomething()并将子类作为参数传进去
      doSomthing(triangle);
      doSomthing(line);
    }
}   
```

对doSomthing()的调用会自动地正确处理，而不管对象的确切类型，比如```doSomthing(circle);```  由于Circle可以被doSomething()看作是Shape，也就是说，doSomthing()可以发送给Shape的任何消息，Circle也可以接收。

## 八、Object类

> 在Java中所有的类最终都继承自单一的基类，这个类就是Object，这称为单根继承结构
>
> 在单根继承结构中的所有对象都具有一个共有接口，所以它们归根到底都是相同的基本类型。
> 
> 单根继承结构保证所有的对象都具有某些功能。所有对象都可以很容易地在堆上创建，而参数传递也得到了
> 极大的简化；并且使垃圾回收器变得容易得多（垃圾回收器正是Java相对C++的重要改进之一） 

## 九、容器

> 创建一种对象类型。这种新的对象类型持有其他对象的应用。这个通常通常被称为容器
>
> Java中具有满足不同需要的各种类型的容器，List（用于存储序列），Map（用来建立对象之间的关联），Set（每中对象类型只持有一个），以及诸如队列、树、堆栈等更多的构件

通常，程序总是根据运行是才知道的某些条件去创建新对象。在此之前，不会知道所需对象的数量，甚至不知道确切的类型。为了解决这个普通的编程问题， 需要在任意时刻和任意位置创建任意数量的对象。所以，就不能依靠创建命名的引用持有每一个对象：MyType aReference ，因此你不知道实际上会需要多少这样的引用

大多数语言都提供某种方法来解决这个基本问题。Java有多种方式保存对象（应该说是对象的引用）。例如数组，可以保存基本类型数据，但数组具有固定的尺寸。但大多数情况并不清楚需要多少个对象，因此数组尺寸固定这一限制显得过于受限了。

Java使用类库提供了容器解决这个问题。其中基本的类型是List、Set、Queue和Map。这些对象类型称为集合类。也称为容器。容器具有一些特性，如Set对于每个值都保存一个对象，Map是允许将某些对象与其他一些对象关联起来的关联数组，Java容器还可以自动调整自己的尺寸

### 泛型和类型安全的容器

```java
class Apple{
    private static long counter;
    private final long id = counter++;
    public long id(){
        return id;
    }
}

class Orange{}

public class AppleAndOrangesWithoutGenerics {
    public static void main(String[] args) {
        ArrayList apples = new ArrayList();
        for(int i = 0; i < 3; i++){
            apples.add(new Apple());
        }
        apples.add(new Orange());
        for(int i = 0;i < apples.size();i++){
            ((Apple)apples.get(i)).id();
        }
    }
}
```

上面的例子中：Apple和Orange类是有区别的，它们除了都是Object之外没有任何共性（记住，如果一个类没有显式地声明继承自哪个类，那么它自动地继承自Object）。因此ArrayList保存的是Object，因为不仅可以通过ArrayList的add()方法将Apple对象放进这个容器，还可以添加Orange对象，而且编译期和运行期都没有问题。但当你用ArrayList的get()方法取出你认为的Apple对象时，得到的只是Object引用，必须将其转型为Apple，因此，需要将整个表达式扩起来，在调用Apple的id()方法之前，强制执行类型。否则，会得到语法错误。但运行时，当你试图将Orange对象转型为Apple时，会得到错误。

> 如果要想定义用来保存Apple对象的ArrayList，你可以声明ArrayList<Apple>，而不仅仅只是ArrayList，其中尖括号括起来的是类型参数（可以有多个），它指定了这个容器实例可以保存的类型。通过使用泛型，就可以在编译器防止将错误类型的对象放置到容器中。

```java
class Apple{
    private static long counter;
    private final long id = counter++;
    public long id(){
        return id;
    }
}
class Orange{}
public class ApplesAndOrangesWithGenerics {
    public static void main(String[] args) {
        ArrayList<Apple> apples = new ArrayList<>();
        for(int i = 0; i < 3;i++){
            apples.add(new Apple());
        }
        for(int i = 0; i < apples.size();i++){
            System.out.println(apples.get(i).id());
        }

        for(Apple c : apples){
            System.out.println(c.id);
        }
    }
}
```
## 十、泛型

在JavaSE5之前，容器存储的对象都只具有Java中的通用类型：Object，由于只能存储object类型，所以当将对象引用置入容器时，必须被向上转型为Object，因此会丢失其身份，当把它取回时，就获取了一个对Object对象的引用，而不是对置入时那个类型的对象的引用。所以怎样才能将它变回先前置入容器中时的具有实用接口的对象呢？

这里要用到向下转型为更具体的类型，这种转型方式是向下转型。我们知道，向上转型是安全的，然而向下转型是不安全的，如果向下转型为错误的类型，就会得到被称为异常的运行时错误。

> 创建容器时，就确定要容器要保存的对象的类型，从而不需要向下转型以及消除犯错误的可能。这种解决方案被称为参数化类型机制。一对尖括号，中间包含类型信息，通过这些特征就可以识别对泛型的使用
> `ArrayList<Shape> shapes = new ArrayList<Shape>();`

现在，编译器可以组织你将Orange放置到apples中，因此它变成了一个编译期错误，而不再是运行时错误。

并且，在将元素从List取出时，类型转换也不再是必需的了。因为List知道它保存的是什么类型，因此它会在调用get()时替你执行转型。这样，通过使用泛型，你不仅知道编译器将会检查你放置到容器中的对象类型，而且在使用容器中的对象时，可以使用更加清晰的语法

上面的例子还说明，如果不需要使用每个元素的索引，可以使用foreach语法来选择List中的每个元素

当指定了某个类型作为泛型参数时，并不仅限于只能将该确切类型的对象放置到容器中，向上转型也可以像作用于其他类型一样作用于泛型

```java
class Apple{
    private static long counter;
    private final long id = counter++;
    public long id(){
        return id;
    }
}
class GrannySmith extends Apple{}
class Gala extends Apple{}
class Fuji extends Apple{}
class Braeburn extends Apple{}
public class GenericsAndUpcasting {
    public static void main(String[] args) {
        ArrayList<Apple> apples = new ArrayList<>();
        apples.add(new GrannySmith());
        apples.add(new Gala());
        apples.add(new Fuji());
        apples.add(new Braeburn());
        for(Apple c : apples){
            System.out.println(c);
        }
    }
}
```

因此，可以将Apple的子类型添加到被指定保存Apple对象的容器中。
程序的输出是从Object默认的toString()方法产生的，该方法将打印类名，后面跟随者该对象的散列码的无符号十六进制表示（这个散列码是通过hashCode()方法产生的）

### 基本概念

Java容器类类库的用途是“保存对象”，并将其划分两个不同的概念：
1）Collection。一个独立元素的序列，这些元素都服从一条或多条规则。List必须按照插入的顺序保存元素，而Set不能有重复元素。Queue按照排队规则来确定对象产生的顺序（通常于它们被插入的顺序相同）
2）Map。一组成对的“键值对”对象，允许你使用键来查找值。ArrayList允许你使用数字来查找值，因此在某种意义上讲，它将数字与对象关联在了一起。Map允许我们使用另一个对象来查找某个对象

可以像下面这样创建一个list，通过使用接口的方式并在创建的时候指定精确类型，此时ArrayList已经被向上转型为List
List<Apple> apples = new ArrayList<>();

因为某些类具有额外的功能，例如，LinkedList具有在List接口中未包含的额外方法，而TreeMap也具有在Map接口中未包含的方法，如果你需要使用这些方法，就不能将它们向上转型为更通用的接口

Collection接口概括了序列的概念--一种存放一组对象的方式。下面的例子用Integer对象填充了一个Collection（用ArrayList表示），然后打印所产生的容器中的所有元素：

```java
public class SimpleCollection {
    public static void main(String[] args) {
        Collection<Integer> c = new ArrayList<>();
        for(int i = 0;i < 10;i++){
            c.add(i);
        }
        for(Integer i:c){
            System.out.println(i + ", ");
        }
    }
}
```

### 添加一组元素

Arrays.asList()方法接受一个数组或是一个用逗号分隔的元素列表（使用可变参数），并将其转换成为一个List对象。

Collection.addAll()方法接受一个Collection对象，以及一个数组或是一个用逗号分隔的列表，将元素添加到Collection中。

```java
public class AddingGroups {
    public static void main(String[] args) {
        Collection<Integer> collection = new ArrayList<>(Arrays.asList(1,2,3,4,5));
        Integer[] moreInts = {6,7,8,9,10};
        collection.addAll(Arrays.asList(moreInts)); // Arrays.asList()方法接受一个数组或是一个用逗号分隔的元素列表（使用可变参数），并将其转换成为一个List对象。
        Collections.addAll(collection,11,12,13,14,15); //Collection.addAll()方法接受一个Collection对象，以及一个数组或是一个用逗号分隔的列表，将元素添加到Collection中。
        Collections.addAll(collection,moreInts);
        List<Integer> list = Arrays.asList(16,17,18,19,20);
        list.set(1,99);
    }
}
```

### 容器的打印

必须使用Arrays.toString()来产生数组的可打印表示，但是打印容器不需要其他帮助

```java
public class PrintingContainers {
    static Collection fill(Collection<String> collection){
        collection.add("rat");
        collection.add("cat");
        collection.add("dog");
        collection.add("dog");
        return collection;
    }

    static Map fill(Map<String,String> map){
        map.put("rat","Fuzzy");
        map.put("cat","Rags");
        map.put("dog","Bosco");
        map.put("dog","Spot");
        return map;
    }

    public static void main(String[] args) {
        System.out.println(fill(new ArrayList<>()));
        System.out.println(fill(new LinkedList<>()));
        System.out.println(fill(new HashSet<>()));
        System.out.println(fill(new TreeSet<>()));
        System.out.println(fill(new LinkedHashSet<>()));
        System.out.println(fill(new HashMap<>()));
        System.out.println(fill(new TreeMap<>()));
        System.out.println(fill(new LinkedHashMap<>()));
    }
}
/**  输出结果：
[rat, cat, dog, dog]
[rat, cat, dog, dog]
[rat, cat, dog]
[cat, dog, rat]
[rat, cat, dog]
{rat=Fuzzy, cat=Rags, dog=Spot}
{cat=Rags, dog=Spot, rat=Fuzzy}
{rat=Fuzzy, cat=Rags, dog=Spot}
*/
```

查看输出结果会发现，默认的打印行为（使用容器的toString()方法）即可生成可读性很好的结果。Collection打印出来的内容用方括号括住，每个元素由逗号分隔。Map则用大括号括住，键与值由等号联系（键在等号左边，值在右边）

ArrayList和LinkedList都是List类型，从结果可以看出，它们都按照被插入的顺序保存元素。两者的不同之处在于执行某些类型的操作时的性能，而且LinkedList包含额操作也多于ArrayList。

HashSet、TreeSet、LinkedHashSet都是Set类型，输出显示Set中，每个相同的项只有保存一次，但是输出也显示了不同的Set实现存储元素的方式不同。HashSet使用的是相当复杂的方式存储元素。这种技术是最快的获取元素方式，因此，存储的顺序看起来并无实际意义（通常你只会关心某事物是够是某个Set的成员，而不关心它在Set出现的顺序）。如果存储顺序很重要，那么可以使用TreeSet，它按照比较结果的升序保存对象；LinkedHashSet按照被添加的顺序保存对象

Map可以使用键来查找对象，键所关联的对象称为值。对于每一个键，Map只接受存储一次。Map.put(key,value) 方法将增加一个值，并将它与某个键关联起来。Map.get(key) 方法将产生与这个键相关联的值。键和值在Map中的保存顺序并不是它们的插入顺序，因为HashMap实现使用的是一种非常块的算法来控制顺序；TreeMap按照比较结果的升序保存键；而LinkedHashMap则按照插入顺序保存键，同时还保留了HashMap的查询速度

### List

List可以将元素维护在特定的序列中。List接口在Collection的接触上添加了大量的方法，使得可以在List的中间插入和移除元素

有两种类型的List：

1）基本的ArrayList，它擅长随机访问元素，但是List的中间插入和移除元素时比较慢

2）LinkedList，它通过代价较低的在List中间进行插入和删除操作，提供了优化的顺序访问。LinkedList在随机访问方面相对比较慢，但是它的特性集较ArrayList更大

List常见的方法：
contains()方法来确定某个对象是否在列表中。
remove()方法移除一个对象
indexOf()发现对象在List中所处位置的索引编号
equals() 确定一个元素是否属于某个List
subList() 允许从较大的列表中创建处一个片段
containsAll() 判断一个列表是否在某个列表中
retainAll() 一种有效的交集操作
removeAll() 将从List中移除在参数List中的所有元素
addAll() 追加列表到末尾

### 迭代器

迭代器是一个对象，它的工作是遍历并选择序列中的对象。此外迭代器通常被称为轻量级对象：创建它的代价小。Java的Iterator只能单向移动，这个Interator只能用来：
1）使用方法Interator()要求容器返回一个Interator。Interator将准备好返回序列的第一个元素
2）使用next()获得序列中的下一个元素
3）使用hastNext()检查序列中是否还有元素
4）使用remove()将迭代器新返回的元素删除

如果只是向前遍历List，并不打算修改List对象本身，那么foreach语法会显得更加简洁。

Interator还可以移除next()产生的最后一个元素，这意味着调用remove()之前必须先调用next()

ListIterator是一个更加强大的Iterator的子类型，它只能用于各种List类的访问。尽管Iterator只能向前移动，但是ListIterator可以双向移动。它还可以产生相对于迭代器在列表中指向的当前位置的前一个和后一个元素的索引，并且可以使用set()方法替换它访问过的最后一个元素。可以通过调用ListIterator()方法产生一个指向List开始处的ListIterator，并且还可以通过调用ListIterator(n) 方法创建一个一开始就指向列表索引为n的元素出的ListIterator。

### LinkedList

LinkedList在中间插入和移除时比ArrayList更高效，但在随机访问操作方面却要逊色一些，LinkedList还添加了可以使其用作栈、队列或双端队列的方法

getFirst() 返回列表的头（第一个元素），如果列表为空，则报异常
removeFirst() 移除并返回列表的头，而在列表为空时报异常
addFirst() 将某个元素插入到列表的头部
addLast() 将某个元素插入到列表的尾部
removeLast() 移除并返回列表的尾部，而在列表为空时报异常

### Stack

栈通常是指 先进后出（LIFO）的容器，有时也被称为叠加栈，因为最后压入的元素，第一个弹出栈。

LinkedList具有能够直接实现栈所有功能的方法，因此可以直接将LinkedList作为栈使用，不过，有时一个真正的栈更能把事情讲清楚：

```java
public class Stack<T> {
    private LinkedList<T> storge = new LinkedList<>();
    public void push(T v){
        storge.addFirst(v);
    }
    public T peek(){
        return storge.getFirst();
    }
    
    public T pop(){
        return storge.removeFirst();
    }
    
    public boolean empty(){
        return storge.isEmpty();
    }
    
    public String toString(){
        return storge.toString();
    }
}
```

Stack<T> 类名之后的<T>告诉编译器这将是一个参数化类型，而其中类型参数，即在类被使用时将会被实际类型替换的参数，就是T。大体上，这个类是在声明“我们在定义一个可以持有T类型对象stack”，stack是用LinkedList实现的，而LinkedList也被告知它持有T类型对象。注意，push()接受的是T类型的对象，而peek()和pop()将返回T类型的对象。peel()将提供栈顶元素，但是并不将其从栈顶移除，而pop()将移除并返回栈顶元素
注意，如果只需要栈的行为，使用继承就不合适了

使用刚刚创建stack类

```java
public class StackCollision {
    public static void main(String[] args) {
        Stack<String> stack = new Stack<>();
        for(String s:"My dog has fleas".split(" ")){
            stack.push(s);
        }
        while (!stack.empty()){
            System.out.println(stack.pop() + " ");
        }
    }
}
```

### Set

Set不保存重复的元素，Set具有与Collection完全一样的接口，因此没有任何额外的功能。实际上Set就是Collection，只是行为不同（这是继承与多态思想的典型应用：表现不同的行为）

```java
public class SetOfInteger {
    public static void main(String[] args) {
        Random rand = new Random(47);
        Set<Integer> intset = new HashSet<>();
        for(int i = 0; i < 10000; i++){
            intset.add(rand.nextInt(30));
        }
        System.out.println(intset);
    }
}
```

在0-29之间的10000个随机数被添加到Set中，因此你可以想象，每一个数都重复了许多次。但是你可以看到，每一个数只有1个实例出现在结果中。还可以注意到的是，输出的顺序没有任何规律可循，这是由于处于速度原因的考虑，HashSet使用了散列，HashSet所维护的顺序与TreeSet或LinkedHashSet都不同，因为它们具有不同的元素存储方式。TreeSet将元素存储在红-黑树数据结构中，而HashSet使用了散列，LinkedHashSet因为查询速度也使用了散列，但是看起来它使用了链表来维护元素的插入顺序

```java
public class SetOperations {
    public static void main(String[] args) {
        Set<String> set1 = new HashSet<>();
        Collections.addAll(set1,"A B C D E F G H I J K L".split(" "));
        set1.add("M");
        System.out.println("H: " + set1.contains("H"));
        System.out.println("N: " + set1.contains("N"));


        Set<String> set2 = new HashSet<>();
        Collections.addAll(set2,"H I J K L".split(" "));
        System.out.println("set2 in set 1 : " + set1.containsAll(set2));
        set1.remove("H");
        System.out.println("set1 : " + set1);
        System.out.println("set2 in set 1 : " + set1.containsAll(set2));
        set1.removeAll(set2);
        System.out.println("set2 removed from set1: " + set1);
        Collections.addAll(set1,"X Y Z".split(" "));
        System.out.println("'X Y Z' added to set1 : " + set1);
    }
}
```

### Map

检查Java的Random类的随机性。键由Random产生的数字，而值是该数字出现的次数

```java
public class Statistics {
    public static void main(String[] args) {
        Random rand = new Random(47);
        Map<Integer,Integer> m = new HashMap<>();
        for(int i = 0; i < 10000; i++){
            int r = rand.nextInt(20);
            Integer freq = m.get(r);
            m.put(r,freq == null ? 1 : freq + 1);
        }
        System.out.println(m);
    }
}
```

### Queue

队列是一个典型的先进先出（FIFO）的容器，即从容器的一段放入事物，从另一端取出，并且事物放入容器的顺序与取出的顺序是相同。队列常被当作一种可靠的将对象从程序的某个区域传输到另一个区域的途径。队列在并发编程中特别重要。因为它们可以安全地将对象从一个任务传输给另一个任务

LinkedList提供了方法以支持队列的行为，并且它实现了Queue接口，因此LinkedList可以用作Queue的一种实现。通过将LinkedList向上转型为Queue。

```java
public class QueueDemo {
    public static void printQ(Queue queue){
        while (queue.peek() != null){ // peek在不移除的情况下返回队头，在队列为空时候返回null
            System.out.println(queue.remove() + " "); // 移除并返回队头
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Queue<Integer> queue = new LinkedList<>();
        Random random = new Random(47);
        for(int i = 0;i < 10;i++){
            queue.offer(random.nextInt(i + 10)); // 将int转换为Integer对象
        }
        System.out.println(queue);
        Queue<Character> qc = new LinkedList<>();
        for(char c : "Baontosaurus".toCharArray()){
            qc.offer(c); // 与Queue相关联的方法之一，允许的情况下，将一个元素插入到队尾，或者返回false
        }
        System.out.println(qc);
    }
}
```

先进先出描述了最典型的队列规则。队列规则是指在给定一组队列的元素的情况下，确定下一个弹出队列的元素的规则。下一个元素应该是等待时间最长的元素。
优先级队列声明下一个弹出元素是最需要的元素（具有最高的优先级）。PriorityQueue添加到JavaSe5中，是为了提供这种行为的一种自动实现。当在PriorityQueue上调用offer()方法来插入一个对象时，这个对象会在队列中被排序，默认的排序将使用对象在队列中的自然顺序，但是你可以通过提供自己的Comparator来修改这个顺序。PriorityQueue可以确保当你调用peek()、poll()和remove()方法时，获取的元素将是队列中优先级最高的元素

```java
public class PriorityQueueDemo {
    public static void main(String[] args) {
        PriorityQueue<Integer> priorityQueue = new PriorityQueue<>();
        Random rand = new Random(47);
        for(int i = 0; i < 10;i++){
            priorityQueue.offer(rand.nextInt(i + 10));
        }
        QueueDemo.printQ(priorityQueue);
        List<Integer> ints = Arrays.asList(25,22,20,18,14,9,3,1,1,2,3,9,14,18,21,23,25);
        priorityQueue = new PriorityQueue<>(ints);
        QueueDemo.printQ(priorityQueue);

        priorityQueue = new PriorityQueue<>(ints.size(), Collections.reverseOrder());
        priorityQueue.addAll(ints);
        QueueDemo.printQ(priorityQueue);

        String fact = "EDUCATION SHOULD ESCHEW OBFUSCATION";
        List<String> strings = Arrays.asList(fact.split(" "));
        PriorityQueue<String> springPQ = new PriorityQueue<>(strings);
        QueueDemo.printQ(springPQ);
        springPQ = new PriorityQueue<>(strings.size(),Collections.reverseOrder());
        springPQ.addAll(strings);
        QueueDemo.printQ(springPQ);

        Set<Character> charSet = new HashSet<>();
        for(char c: fact.toCharArray()){
            charSet.add(c);
        }

        PriorityQueue<Character> characterPQ = new PriorityQueue<>(charSet);
        QueueDemo.printQ(characterPQ);

    }
}
```

### Foreach与迭代器

```java
public class ForEachCollections {
    public static void main(String[] args) {
        Collection<String> cs = new LinkedHashSet<>();
        Collections.addAll(cs,"Take the long way home".split(" "));
        for(String s:cs){
            System.out.println("'" + s + "'");
        }
    }
}
```

上面的代码中cs是一个Collection，所以这段代码展示了能够与foreach一起工作是所有Collection对象的特性。
之所以能够工作，是因为JavaSE5引入了新的被称为Iterable的接口，该接口包含一个能够产生Iterator的iterator()方法，并且Iterable接口被foreach用来在序列中移动。如果创建了任何实现Iterable的类，都可以将它用于foreach语句中

```java
public class EnvironmentVariables {
    public static void main(String[] args) {
        for(Map.Entry entry:System.getenv().entrySet()){ // System.getenv()返回一个Map， entrySet()产生一个由Map.Entry的元素构成的Set
            System.out.println(entry.getKey() + "; " + entry.getValue());
        }
    }
}
```

foreach 与数组

```java
public class ArrayIsNotIterable {
    static <T> void test(Iterable<T> ib){
        for(T t: ib){
            System.out.println(t + " ");
        }
    }

    public static void main(String[] args) {
        test(Arrays.asList(1,2,3));
        String[] strings = {"A","B","C"};
        test(Arrays.asList(strings));
    }
}
```

## 十一、存储位置

1）寄存器 最快的存储区，位于处理器内部。寄存器的数量极其优先，所以寄存器根据需求进行分配，不能直接控制，在程序中也不能感觉到寄存器存在的任何迹象

2）堆栈 位于RAM（随机访问存储器）中，可以通过堆栈指针从处理器获取直接支持。堆栈指针向下移动，则分配新的内存；向上移动，则释放哪些内存。这是一种仅次于寄存器的有效的分配存储方法。对象引用存储在堆栈中

3）堆 一种通用的内存池，位于RAM中，用于存放所有的Java对象

4）常量存储 常量值通常直接存放在程序代码内部。

5）非RAM存储 数据完全存活于程序之外，可以不受程序的任何控制，在程序没有运行时也可以存在。其中两个基本的例子是流对象和持久化对象。流对象中，对象转化成字节流，通常被发送给另一台机器。持久化对象中，对象被存放于磁盘上。这种存储方式的技巧在于：把对象转化成可以存放在其他媒介上的事物，在需要时，可恢复成常规的、基于RAM的对象

## 十二、数据类型

> 数据类型包含两种：基本数据类型和引用数据类型
> 
> 整数类型四种表示形式：十进制 、八进制 以0开头、二进制 0b或0B开头、十六进制 0x或0X开头
>
> 浮点类型两种表示形式：十进制数形式、科学记数法形式 
  
![](https://upload-images.jianshu.io/upload_images/2765653-5be4860ad470d9bf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Java中一般通过new创建对象并将对象存储在“堆”里，并通过变量引用保存对象的地址，而对于基本类型，需要特殊对待，基本类型不用new来创建变量，而是创建一个并非是引用的“自动”变量。这个变量直接存储的是“值”，并置于堆栈中，因此更加高效

Java会确定每种基本类型所占存储空间的大小，并且这个大小并不会随着机器硬件架构的变化而变化。这也成为了Java比其他大多数语言编写的程序更具移植性的原因之一

![](https://upload-images.jianshu.io/upload_images/2765653-bde027253732542f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

1个字节占8bits，所以

![](https://upload-images.jianshu.io/upload_images/2765653-aa40d1900172a433.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> float单精度类型，尾数精确到7位，double双精度类型，尾数精确到14位
> 
> float和double不适合在不容许舍入误差的金融计算领域，如果需要进行不产生舍入误差的精确数字计算，需要使用BigDecimal
>  
> folat类型的数值后面要有一个后缀F或f，没有的默认为double类型，也可以在数值后添加后缀D或者d，明确double类型
>
> BigInteger可以准确的表示任何大小的整数值，而且不会丢失任何消息
> 
> BigDecimal支持任何精度的浮点数，例如，可以用它进行精确的货币计算

## 十三、作用域

> 作用域决定了在其内定义的明亮名的可见性和生命周期，**在Java中，作用域由花括号的位置决定**

###  基本类型的作用域

```java

public class Test{
    {int x = 12;
    // Only x available
        {
        int q = 96;
        // Bath x & q available
        }
    // Only x available
    // q is "out of scope"
    }
}
```

###  对象的作用域

> Java对象不具备和基本类型一样的生命周期，当用new创建一个Java对象时，它可以存活于作用域之外

```java

public class Test{
    {
      String s = new String("a string"); 
    } // End of scope
}
```

引用s在作用域终点就消失了，然而，s指向的String对象仍继续占据内存空间。在上面的代码中，我们无法在这个作用域之后访问这个对象，因为对它唯一的引用已超出了作用域的范围，而对象的回收，是通过Java的垃圾回收器，它用来监视用new创建的所有对象，并辨别哪些不会再被引用的对象，随后，释放这些对象的内存空间，以便供其他新的对象使用


## equals()重写

```java
class Value{
    int i;
}

public class EqualMethod2{
    public static void main(String[] args){
        Value v1 = new Value();
        Value v2 = new Value();
        v1.i = 100;
        v2.i = 100;
        System.out.println(v1.equals(v2));
    }
}

// Output
// false
```

当我们用自己创建的类，使用equals()方法来比较，虽然v1和v2两个引用不同，但对象内容是相同的，而且equals()比较的是对象内容的值，但结果确实false。这是由于equals()的默认行为是比较引用。所以除非在自己的新类中覆盖equals()方法，否则比较的还是引用

## 控制执行流程

就像有知觉的生物一样，程序必须在执行过程中控制它的世界，并做出选择。在Java中，要使用执行控制语句来做出选择。

在Java中，控制语句涉及的关键字包括if-else、while、do-while、for、return、break以及选择语句switch。

### true和false

> 所有条件语句都利用条件表达式的true或false来决定执行路径。要注意的是Java不允许我们将一个数字作为布尔值使用。

### if-else

if-else语句是控制程序流程的最基本的形式。其中else是可选的，所以可以按下述两种形式来使用if：

布尔表达式必须产生一个布尔结果，statement指用分号结尾的简单语句 或复合语句—封闭在花括号内的一组简单语句。

```
if(Boolean-expression)// 布尔表达式必须产生一个布尔结果
    statement // 用分号结尾的简单语句

```

或

```
if(Boolean-expression){ 
    statement 
}else{
    statement
}

```
或

```
if(Boolean-expression){ 
    statement 
}else if(Boolean-expression){
    statement
}else{
    statement
}
```

### 迭代

> while、do-while和for用来控制循环，称为迭代语句。语句会重复执行，直到起控制作用的布尔表达式得到false的结果为止。

#### while 与 do-while

while和do-while唯一的区别就是do-while中的语句至少会执行一次，
即便表达式第一次就被计算为false。而在while循环结构种，如果条件第一次就为false，
那么其中的语句根本不会执行。在实际应用中，while比do-while更常用一些


```
// 在循环刚开始时，会计算一次布尔表达式的值；而在语句的下一次迭代开始前会再计算一次
while(Boolean-expression){
    statement
}
```

```
do{
    statement
}while(Boolean-expression)
```


#### for 循环语句

> for循环第一次迭代之前要进行初始化。随后，它会进行条件测试，而且在每一次迭代结束时，进行某种形式的“步进”。
> 
> 初始化表达式(initializaion) 布尔表达式(Boolean-expression) 或者步进(step)运算，都可以为空，
> 全部为空作用相当于while，但分号不能省略。
>
> 每次迭代前会测试布尔表达式。若获得的结果是false，就会执行for语句后面的代码行。每次循环结束，会执行一次步进。

```
for(initializaion;Boolean-expression;step){
    statement
}
```

```java
class MyTest{
    public static void main(String[] args){
        for(char c = 0; c < 128;c++){
           if(Charscter.isLower(c)){
                System.out.println("value: " + (int)c + " character: " + c);
            }   
        }
    }
}
```

注意：变量c是在程序用到它的地方被定义的，也就是在for循环的控制表达式里，而不是在main()开始的地方定义的。c的作用于就是for控制的表达式的范围内。

#### 逗号操作符

逗号操作符(注意不是逗号分隔符，逗号用作分隔符时用来分隔函数的不同参数)，Java里唯一用到逗号操作符的地方就是for循环的控制表达式。在控制表达式的初始化和步进控制部分，可以使用一系列由逗号分隔的语句；而且那些语句均会独立执行。

通过使用逗号操作符，可以在for语句内定义多个变量，但是它们必须具有相同的类型

```java
class MyTest{
    public static void main(String[] args){
        for(char c = 0; c < 128;c++){
            for(int i = 1,j = i + 10; i < 5; i ++,j = i * 2){
                System.out.println("i = " + i + " j = " + j);
            }
        }
    }
}
```

#### Foreach语法

> Java SE5引入了一种新的更加简洁的for语法用于数组和容器，即foreach语法，表示不必创建int变量去对由访问项构成的序列进行计数，foreach将自动产生每一项
> 
> for(float x : f) 这条语句定义了一个float类型的变量x，继而将每一个的f的元素赋值给x

```java
class MyTest{
    public static void main(String[] args){
        Random rand = new Random(47);
        float f[] = new float[10];
        for(int i = 0; i < 10; i++){
          f[i] = rand.nextFloat();
        }
        for(float x : f){
          Sytem.out.println(x);
        }
    }
}
```

- String使用Foreach

String类有一个方法toCharArray()，它返回一个char数组，因此可以迭代在字符串里面的所有字符：

```java
class MyTest{
    public static void main(String[] args){        
        for(char c : "An African Swallow".toCharArray()){
            System.out.println(c + " ");
        }
    }
}
```


### return

> return关键词有两方面的用途：一方面指定一个方法返回什么值（假设它没有void返回值），
> 另一方面它会导致当前的方法退出，并返回那个值。
> 
> 如果在返回void的方法中没有returan语句，那么在该方法的结尾处会有一个隐式的return，
> 因为在方法中并非总是必须要有一个return语句。
>
> 但是，如果一个方法声明它将返回void之外的其他东西，那么必须确保每一条代码路径都将返回一个值


```java
class MyTest{
    static int test(int testval,int target){
        if(testval > target){
            return 1;
        }else if(testval < target){
            return -1;
        }else{
            return 0;
        }        
    }
    public static void main(String[] args){  
        System.out.println(test(10,5));
        System.out.println(test(5,10)); 
        System.out.println(test(5,5));      
    }
}
```


### break和continue

> 在任何迭代语句的主题部分，都可用break和continue控制循环的流程。其中breank用于强行退出循环，不执行循环中剩余的部分。而continue则停止执行当前的迭代，然后退回循环循环起始处，开始下一次迭代

```java
public class MyTest01 {
    public static void main(String[] args){
        for(int i = 0;i < 100;i++){
            if(i == 74){
                break;
            }
            if(i % 9 != 0){
                continue;
            }
            System.out.print(i + " ");
        }

        System.out.println();
        int i = 0;
        while (true){
            i ++;
            int j = i * 27;
            if(j == 1269){
                break;
            }
            if(i % 10 != 0){
                continue;
            }
            System.out.print(i + " ");
        }
    }
}
```

例子中还可以看到“无穷循环”的情况。然而，循环内容有一个break语句，可中止循环。除此之外，continue语句执行序列回到循环的开头，而没有去完成continue语句之后的所有内容。

无穷循环的第二种形式是for(;;)。编译器将while(true)与for(;;)看作是同一回事。所以具体选用哪个取决于自己的编程习惯

###  switch

> switch 有时也被划归为一种选择语句。根据整数表达式的值，switch语句可以从一系列代码中选出一段去执行。

```
switch(integral-selector){
    case integral-value1 : statement;break;
    case integral-value2 : statement;break;
    case integral-value3 : statement;break;
    case integral-value4 : statement;break;
    case integral-value5 : statement;break;
    default: statement;
}
```

其中，integral-selector是一个能够产生整数值的表达式，switch能将这个表达式的结果与每个integral-value相比较。若发现一致，就执行对应的语句（单一语句或多条语句，其中并不需要括号）。若没有发现一致的，就执行default(默认)语句。

在上面的定义中，大家会注意到每个case均以一个break结尾，这样可使执行流程跳转至switch主体的末尾。这是构建switch语句的一种传统方式，但break是可选的。若省略break，会继续执行后面的case语句，直到遇到一个break为止。注意最后的default语句没有break，因为执行流程已到了break的跳转目的地。

switch要求使用一个integral-selector，并且必须是int或char那样的整数值。例如，若将一个字符串或者浮点数作为选择因为使用，那么它们在switch语句里是不会工作的。对于非整数类型，则必须使用一系列if语句。

```java
public class MyTest01 {
    public static void main(String[] args){
        // switch练习
        Random rand = new Random(47);
        for(int i = 0; i < 10; i++){
            int c = rand.nextInt(26) + 'a';
            System.out.print((char)c + ", " + c + ": ");
            switch (c){
                case 'a':
                case 'e':
                case 'i':
                case 'o':
                case 'u': System.out.println("vowel");break;
                case 'y':
                case 'w': System.out.println("Sometimes a vowel");break;
                default: System.out.println("consonant");
            }
        }
    }
}
// Output:
// y, 121: Sometimes a vowel
// n, 110: consonant
// z, 122: consonant
// b, 98: consonant
// r, 114: consonant
// n, 110: consonant
// y, 121: Sometimes a vowel
// g, 103: consonant
// c, 99: consonant
// f, 102: consonant
```

## 用构造器确保初始化

> 在Java中，通过构造器，可以确保每个对象都会得到初始化。
> 创建对象时，如果类具有构造器，Java就自动调用相应的构造器，从而保证了初始化的进行。
> 
> 构造器的命名：构造器采用与类相同的名称
> 这里要注意的是，构造器的名称必须与类名完全相同，所以每个方法首字母小写的规则并不适用于构造器


```java
class Rock{
    // 不接受任何参数的构造器叫做"默认构造器"
    Rock(){
        System.out.println("Rock ");
    }
    public static void main(String[] args) {
        for(int i = 0;i < 3; i++){
            new Rock();
        }
    }
}
```

> 上面例子中初始化的过程
> 现在创建对象时：new Rock();
> 1）将会为对象分配存储空间，并调用相应的构造器
> 2）这就确保了在操作对象之前，它已经被正确的初始化了

### 默认构造器

> 默认构造器（又名无参构造器）是没有形式参数的
> 
> 无参构造器的作用是创建一个默认对象。如果你的写的类中没有构造器，则编译器会自动帮你
> 创建一个默认构造器

```java
class Test03{}
class Test04{
    public static void main(String[] args) {
        Test03 test03 = new Test03();
    }
}
```

new test03() 创建了一个新对象，并调用默认构造器，即使没有明确定义

> 但如果已经定义了一个构造器（无论是否有参数），编译器都不会帮你自动创建默认构造器

```java
class Test03{    
    Test03(int i){}
    Test03(double d){}
}
class Test04{
    public static void main(String[] args) {
        // Test03 test01 = new Test03(); // 编译器会报错
        Test03 test02 = new Test03(1);
        Test03 test03 = new Test03(1.0);
    }
}
```


### 有参构造器

> 构造器也能带有形式参数，以便指定如何创建对象

```java
class MyTest02{
    static int test(int testval,int target){
        if(testval > target) {
            return 1;
        }
        return 0;
    }
}
class Rock{
    Rock(int i){
        System.out.println("Rock " + i + " ");
    }
    public static void main(String[] args) {
        for(int i = 0;i < 3; i++){
            new Rock(i);
        }
    }
}
```

> 构造器是一种特殊类型的方法，因为他没有返回值，这与返回值为空（void）明显不同。对于空
> 返回值，尽管方法本身不会自动返回什么，但仍可选择让它返回别的东西。
>
> 构造器则不会返回任何东西。
> 
> 但new表达式确实了返回了新建对象的引用，但构造器本身并没有任何返回值

## 方法重载

> 在Java里，构造器的强制重载方法名的另一个原因。既然构造器的名字已经由类名所决定，就只能有一个构造器名，
> 如果想用多种方式创建一个对象怎么办呢？这就需要两个构造器：一个默认构造器，另一个带有参数的构造器。由于都是
> 构造器，所以它们必须有相同的名字，即类名。为了让方法名相同而形式参数不同的构造器同时存在，必须用到方法重载。
> 同时，尽量方法重载是构造器所必须的，但也可应用于其他方法，且用法同样方便。

```java
class Tree{
    int height;
    Tree(){
        System.out.println("Planting a seeding");
        height = 0;
    }

    Tree(int initialHeight){
        height = initialHeight;
        System.out.println("Creating new Tree that is " + height + " feel tall");
    }

    void info(){
        System.out.println("Tree is " + height+ " feet tall");
    }

    void info(String s){
        System.out.println(s + ": Tree is " + height + " feet tall");
    }

    public static void main(String[] args) {
        for(int i = 0; i < 3; i++){
            Tree t = new Tree(i);
            t.info();
            t.info("overloaded method");
        }
        new Tree();
    }
}
// Output
// Creating new Tree that is 0 feel tall
// Tree is 0 feet tall
// overloaded method: Tree is 0 feet tall
// Creating new Tree that is 1 feel tall
// Tree is 1 feet tall
// overloaded method: Tree is 1 feet tall
// Creating new Tree that is 2 feel tall
// Tree is 2 feet tall
// overloaded method: Tree is 2 feet tall
// Planting a seeding
```

### 如何区分重载方法

> 要是几个方法有相同的方法，Java如何才能知道你指的是哪一个呢？
>
> 其实规则很简单：每个重载的方法都必须有一个独一无二的参数类型列表，对于名字相同的方法，除了
> 参数类型的差异以外，甚至参数顺序的不同也足以区分两个方法（不过，一般情况下别这么做，因为这会使代码难以维护）

```java
// 区分重载方法
class OverLoadingOrder{
    static void f(String s,int i){
        System.out.println("String: " + s + ", int: " + i);
    }
    static void f(int i, String s){
        System.out.println("int: " + i + ", String: " + s);
    }
    public static void main(String[] args) {
        f("String first",11);
        f(99,"Int first");
    }
}
```

### 基本类型的重载

> 在下面的例子中我们可以看到：数值5会被当作int值处理，所以如果有某个重载方法接收int类型参数，它就会被调用
> 
> 由此可以说明：如果传入的数据类型（实际的参数类型）小于声明中形式参数类型，实际数据类型就会被提升
>
> 但要注意的是，char型不同，如果无法找到接收char参数的方法，就会把cahr类型直接提升到int型

```java
/**
* 在PrimitiveOverloading中，分别创建了f1、f2、f3、f4、f5、f6、f7  
* 和testConstVal、testChar、testByte、testShort、testInt、testLong、testFloat、testDouble 用来测试传入不同基本类型给重载方法如何处理
* 
* 
* 每个方法都有自己的重载方法。
* 
*/ 
class PrimitiveOverloading{

    void f1(char x){
        System.out.print("f1(char)");
    }
    void f1(byte x){
        System.out.print("f1(byte)");
    }
    void f1(short x){
        System.out.print("f1(short)");
    }
    void f1(int x){
        System.out.print("f1(int)");
    }
    void f1(long x){
        System.out.print("f1(long)");
    }
    void f1(float x){
        System.out.print("f1(float)");
    }
    void f1(double x){
        System.out.print("f1(double)");
    }

    void f2(byte x){
        System.out.print("f2(byte)");
    }
    void f2(short x){
        System.out.print("f2(short)");
    }
    void f2(int x){
        System.out.print("f2(int)");
    }
    void f2(long x){
        System.out.print("f2(long)");
    }
    void f2(float x){
        System.out.print("f2(float)");
    }
    void f2(double x){
        System.out.print("f2(double)");
    }


    void f3(short x){
        System.out.print("f3(short)");
    }
    void f3(int x){
        System.out.print("f3(int)");
    }
    void f3(long x){
        System.out.print("f3(long)");
    }
    void f3(float x){
        System.out.print("f3(float)");
    }
    void f3(double x){
        System.out.print("f3(double)");
    }

    void f4(int x){
        System.out.print("f4(int)");
    }
    void f4(long x){
        System.out.print("f4(long)");
    }
    void f4(float x){
        System.out.print("f4(float)");
    }
    void f4(double x){
        System.out.print("f4(double)");
    }

    void f5(long x){
        System.out.print("f5(long)");
    }
    void f5(float x){
        System.out.print("f5(float)");
    }
    void f5(double x){
        System.out.print("f5(double)");
    }

    void f6(float x){
        System.out.print("f6(float)");
    }
    void f6(double x){
        System.out.print("f6(double)");
    }

    void f7(double x){
        System.out.print("f7(double)");
    }

    void testConstVal(){
        System.out.print("5: ");
        f1(5);f2(5);f3(5);  f4(5);f5(5); f6(5); f7(5);
    }

    void testChar(){
        char x = 'x';
        System.out.print("char:");
        f1(x);f2(x);f3(x);f4(x);f5(x);f6(x);f7(x);
    }

    void testByte(){
        byte x = 0;
        System.out.print("byte: ");
        f1(x);f2(x);f3(x);f4(x);f5(x);f6(x);f7(x);
    }

    void testShort(){
        short x = 0;
        System.out.print("short : ");
        f1(x);f2(x);f3(x);f4(x);f5(x);f6(x);f7(x);
    }

    void testInt(){
        int x = 0;
        System.out.print("int : ");
        f1(x);f2(x);f3(x);f4(x);f5(x);f6(x);f7(x);
    }

    void testLong(){
        long x = 0;
        System.out.print("long: ");
        f1(x);f2(x);f3(x);f4(x);f5(x);f6(x);f7(x);
    }

    void testFloat(){
        float x = 0;
        System.out.print("float: ");
        f1(x);f2(x);f3(x);f4(x);f5(x);f6(x);f7(x);
    }

    void testDouble(){
        double x = 0;
        System.out.print("double: ");
        f1(x);f2(x);f3(x);f4(x);f5(x);f6(x);f7(x);
    }

    public static void main(String[] args) {
        PrimitiveOverloading p = new PrimitiveOverloading();
        p.testConstVal();
        System.out.println();
        p.testChar();
        System.out.println();
        p.testByte();
        System.out.println();
        p.testShort();
        System.out.println();
        p.testInt();
        System.out.println();
        p.testLong();
        System.out.println();
        p.testFloat();
        System.out.println();
        p.testDouble();
    }
}
// Output
// 5: f1(int)f2(int)f3(int)f4(int)f5(long)f6(float)f7(double)
// char:f1(char)f2(int)f3(int)f4(int)f5(long)f6(float)f7(double)
// byte: f1(byte)f2(byte)f3(short)f4(int)f5(long)f6(float)f7(double)
// short : f1(short)f2(short)f3(short)f4(int)f5(long)f6(float)f7(double)
// int : f1(int)f2(int)f3(int)f4(int)f5(long)f6(float)f7(double)
// long: f1(long)f2(long)f3(long)f4(long)f5(long)f6(float)f7(double)
// float: f1(float)f2(float)f3(float)f4(float)f5(float)f6(float)f7(double)
// double: f1(double)f2(double)f3(double)f4(double)f5(double)f6(double)f7(double)
```

> 但如果传入的实际参数大于重载方法声明的形式参数，方法接受较小的基本类型作为参数，如果传入的实际参数较大，
> 就得通过类型转换来执行窄化转换。如果不这么做，编译器就会报错

```java
// 基本类型的重载，窄化处理
class Demotion{

    void f1(char x){
        System.out.print("f1(char)");
    }
    void f1(byte x){
        System.out.print("f1(byte)");
    }
    void f1(short x){
        System.out.print("f1(short)");
    }
    void f1(int x){
        System.out.print("f1(int)");
    }
    void f1(long x){
        System.out.print("f1(long)");
    }
    void f1(float x){
        System.out.print("f1(float)");
    }
    void f1(double x){
        System.out.print("f1(double)");
    }

    void f2(byte x){
        System.out.print("f2(byte)");
    }
    void f2(short x){
        System.out.print("f2(short)");
    }
    void f2(int x){
        System.out.print("f2(int)");
    }
    void f2(long x){
        System.out.print("f2(long)");
    }
    void f2(float x){
        System.out.print("f2(float)");
    }
    void f2(double x){
        System.out.print("f2(double)");
    }

    void f3(short x){
        System.out.print("f3(short)");
    }
    void f3(int x){
        System.out.print("f3(int)");
    }
    void f3(long x){
        System.out.print("f3(long)");
    }
    void f3(float x){
        System.out.print("f3(float)");
    }
    void f3(double x){
        System.out.print("f3(double)");
    }

    void f4(int x){
        System.out.print("f4(int)");
    }
    void f4(long x){
        System.out.print("f4(long)");
    }
    void f4(float x){
        System.out.print("f4(float)");
    }
    void f4(double x){
        System.out.print("f4(double)");
    }

    void f5(long x){
        System.out.print("f5(long)");
    }
    void f5(float x){
        System.out.print("f5(float)");
    }
    void f5(double x){
        System.out.print("f5(double)");
    }

    void f6(float x){
        System.out.print("f6(float)");
    }
    void f6(double x){
        System.out.print("f6(double)");
    }

    void f7(double x){
        System.out.print("f7(double)");
    }


    void testDouble(){
        double x = 0;
        System.out.print("double argument: ");
        f1(x);f2((float)x);f3((long)x);f4((int)x);f5((short)x);f6((byte)x);f7((char)x);
    }

    public static void main(String[] args) {
        Demotion p = new Demotion();
        p.testDouble();
    }
}
// Output
// double argument: f1(double)f2(float)f3(long)f4(int)f5(long)f6(float)f7(double)
```

### 以返回值区分重载方法

如果两个方法拥有相同的类名和参数列表，如果考虑用方法的返回值来区分呢？比如现有有两个方法void f(){}和int f(){return1} 只要编译器可以根据语境明确判断出语义，比如在int x = f()中，那么的确可以据此区分重载方法。不过，有时你并不关心刚发的返回值，你想要的是方法调用的其他效果(这常被称为“为了副作用而调用”)，这时你可能会调用方法而忽略其返回值。如果像这样调用方法f();，此时Java如何才能判断该调用哪一个f()呢？别人该如何理解这种代码呢？因此，根据方法的返回值来区分重载方法是行不通的

## this关键字

> 同一个类型的两个对象，分别是a和b，如何才能让这两个类都能调用peel()方法呢？

```java
class Banana{  
    void peel(int i){}
}
class Test01{
    public static void main(String[] args) {
        Banana a = new Banana();
        Banana b = new Banana();
        banana01.peel(1);
        banana02.peel(2);
    }
}
```

编译器会把"所操作对象的引用"作为第一个参数传递给peel()。所以上述两个方法的调用就变成了会这样：

```
Banana.peel(a,1);
Banana.peel(b,2);
```

但这是内部的表现形式，编写代码时并不能这么写。如果想在方法内部获得当前对象的引用。可以通过this关键字，
this 关键字只能只能在方法内部使用，表示对"调用方法的那个对象"的引用。但要注意的是：如果在方法内部调用
同一个类的另一个方法，就不必使用this，直接调用即可。当前方法中的this引用会自动应用于同一个类中的其他方法

```java
class Test{
    void pick(){}
    void pit(){pick();}
}
```

> 可以使用this，在return语句里返回当前对象的引用

```java
class Test{
    int i = 0;
    Leaf increment(){
        i++;
        return this;
    }
    void print(){
        System.out.println("i = " + i);
    }
    public static void main(String[] args){
        Leaf x = new Leaf();
        x.increment().increment().increment().print(); // 由于increment()通过this关键字返回了对当前对象的引用，所以很容易在一条语句里对同一个对象执行多次操作
    }
}
// Output
// i = 3
```

> this关键字对于将当前对象传递给其他方法也很有用

```java
class Person {
     void eat(Apple apple) {
        Apple peeled = apple.getPeeled();
        System.out.println("Yummy");
    }
}
class Peeler {
    static Apple peel(Apple apple) {
        return apple;
    }
}
class Apple {
    Apple getPeeled() {
        return Peeler.peel(this);
    }
    public static void main(String[] args) {
        new Person().eat(new Apple());
    }
}
```

> 通过this在构造器中调用构造器

同一个类可能有多个构造器，可以通过this在构造器中调用构造器，如果在构造器中，为this添加了参数列表。
那么产生对符合参数列表的某个构造器的明确调用。

而且在构造器中只能用this调用一个构造器，并且必须将this调用置于最初始处，否则编译器会报错

```java
class Flower{

    int petalCount = 0;
    String s = "initial value";

    Flower(int petals){
        petalCount = petals;
        System.out.println("Constructor w/ int arg only,petalCount = " + petalCount);
    }

    Flower(String ss){
        System.out.println("Constructor w/ String arg only,petalCount = " + ss);
        s = ss;
    }

    Flower(String s,int petals){
        this(petals);
        //this(s); // 不用调用两个，否则编译器报错
        this.s = s; // 当前对象的s字段
        System.out.println("String & intargs");
    }

    Flower(){
        this("hi" ,47);
        System.out.println("default constructor(no args)");
    }

    void PrintPetalCount(){
        //this(11); // 不能在非构造器使用this
        System.out.println("petalCount = " + petalCount + "s = " + s);
    }

    public static void main(String[] args) {
        Flower x = new Flower();
        x.PrintPetalCount();
    }
}

// Output
// Constructor w/ int arg only,petalCount = 47
// String & intargs
// default constructor(no args)
// petalCount = 47s = hi
```

## static 含义

> static 方法（静态方法）就是没有this的方法。在static方法的内部不能调用非静态方法，反过来是可以的。
> 而且可以在没有创建任何对象的前提下，仅仅通过类本身来调用static方法。

## 成员初始化

> Java 尽力保证：所有变量在使用前都能得到恰当的初始化。对于方法的局部变量，必须在使用时为变量赋一个默认值，
> 否则编译器会报错
> 
> 对于类的数据成员（即字段）是基本类型，如果定义是没有初值，编译器也会给一个初始值，如果是在类里定义一个
> 对象引用时，如果不将其初始化，此引用就会获得一个特殊值null

```java
class InitialValues{
    // 只定义字段不赋值
    boolean t;
    char c;
    byte b;
    short s;
    int i;
    long l;
    float f;
    double d;
    InitialValues reference;
    void printInitialValues(){
        System.out.println("Data type Initial value");
        System.out.println("boolean " + t); // boolean 初始值false
        System.out.println("char " + c); // char 初值为0，所以为空
        System.out.println("byte " + b); // byte 初值为0
        System.out.println("short " + s); // short 初值为0
        System.out.println("int " + i); // int 初值为0
        System.out.println("long " + l); // long 初值为0
        System.out.println("double " + d); // double 初值为0.0
        System.out.println("InitialValues " + reference); // 引用类型reference 初值为null
    }

    public static void main(String[] args) {
        InitialValues initialValues = new InitialValues();
        initialValues.printInitialValues();
        /**
         * 可以使用这种写法
         * new InitialValues.printInitialValues();
         */
    }
}
```

> 指定初始化 就是在定义类成员变量的地方为其赋值

```java
class Depth{}

class InitialValues{
    // 定义字段并赋值
    boolean t = true;
    char c = 'x';
    byte b = 47;
    short s = 0xff;
    int i = 999;
    long l = 1;
    float f = 3.14f;
    double d = 3.14159;
    InitialValues reference;
    Depth dep = new Depth();  // 为引用类型赋值，如果没有指定初始值就尝试使用，会出现运行时错误
}
```

> 通过调用某个方法来提供初值 ，并且这个方法也可以带有参数，但这些参数必须是已经被初始化了的

```java
class MethodInit{
    int i = f(); // 通过调用某个方法来提供初值
    int j = g(i); // 方法可以带已经初始化了的参数
    int f(){
        return 11;
    }
    int g(int n){
        return n * 10;
    }   
}
```

但是这样写会报错：

```java
class MethodInit{

    // int j = g(i); // 会报错 
    int i = f(); // 通过调用某个方法来提供初值
    int f(){
        return 11;
    }
    int g(int n){
        return n * 10;
    }   
}
```

上述程序的正确性取决于初始化的顺序，而与其编译方式无关。所以，编译器会对这种“向前引用”报错。

## 构造器初始化

> 可以用构造器来进行初始化，在运行时刻，可以调用方法或执行某些工作来确定初值，但要牢记：无法
> 组织自动初始化的进行，它将在构造器之前被调用之前发生。

```java
// 构造器初始化   
class Counter{
    int i;
    Counter(){
        i = 7;
    }
}
```

在上面的代码中：i首先会被置为0，然后变成7；对于所有基本类型和对象引用，包括在定义时已经指定初值的变量，这种情况都是成立的。

因此，编译器不会强制你一定要在构造器的某个地方或在使用之前对元素进行初始化，因为初始化早已得到了保证

- 初始化的顺序

```java
// 初始化顺序
class Window {
    Window(int marker) {
        System.out.println("Window" + marker);
    }
}
class House {
    Window w1 = new Window(1);
    House() {
        System.out.println("House()");
        w3 = new Window(33);
    }
    Window w2 = new Window(2);
    void f() {
        System.out.println("f()");
    }
    Window w3 = new Window(3);

    public static void main(String[] args) {
        House h = new House();
        h.f();
    }
}
// Output
// Window1
// Window2
// Window3
// House()
// Window33
// f()
```

在House类中，几个Window对象的定义穿插在方法各处，但运行结果表示所有的变量都在调用构造器和其他方法之间得到初始化

## 静态数据的初始化

> 无论创建多少个对象，讲台数据都只占用一份存储区域。static关键字不能应用于局部变量。因此它只能作用于域。
> 
> 如果一个域是静态的基本类型域，且没有对它进行初始化，那么它就会获得基本类型的标准初值；如果它是一个对象引用，那么它的默认
> 初始化值就是null
> 
> 如果在定义出初始化，采取的方法域非静态数据没什么不同：

```java
class Bowl{
    Bowl(int marker){
        System.out.println("Bowl " + marker);
    }
    void f1(int marker){
        System.out.println("f1 " + marker);
    }
}
class Table{
    static Bowl bowl1 = new Bowl(1);
    Table(){
        System.out.println("Table()");
        bowl2.f1(1);
    }
    void f2(int marker){
        System.out.println("f2 " + marker);
    }
    static Bowl bowl2 = new Bowl(2);
}
class Cupboard{
    Bowl bowl3 = new Bowl(3);
    static Bowl bowl4 = new Bowl(4);
    Cupboard(){
        System.out.println("Cupboard()");
        bowl4.f1(2);
    }
    void f3(int marker){
        System.out.println("f3 " + marker);
    }
    static Bowl bowl5 = new Bowl(5);
}
class StaticInitialization{
    public static void main(String[] args) {
        System.out.println("Creating new Cupboard() in main");
        new Cupboard();
        System.out.println("Creating new Cupboard() in main");
        new Cupboard();
        table.f2(1);
        cupboard.f3(1);
    }
    static Table table = new Table();
    static Cupboard cupboard = new Cupboard();
}
```

由上面的代码可以知道，静态初始化只有在必要时刻才会进行。如果不创建Table对象，也不引用Table.b1或Table.b2，
那么静态的Bowl b1和b2永远都不会被创建。只有在第一个Table对象被创建（或第一次访问静态数据）的时候，它们才会被初始化。并且，此后静态对象不会再次被初始化

> 初始化的顺序是先静态对象（如果它们尚未因对象创建而被初始化），而后“非静态”对象，从输出结果中可以观察到这一点。

## 对象的创建过程*

假如现有有个名为Dog的类：

1）即使没有显示地使用static关键字，构造器实际上也是静态方法。因此，当首次创建类型为Dog的对象时（构造器可以看成静态方法），或者Dog类的静态/静态域首次被访问时，Java解释器必须查找类路径，以定位Dog.class文件

2）然后载入Dog.class，有关静态初始化的所有动作都会执行，因此，静态初始化只在Class对象首次加载的时候进行一次

3）当用new Dog()创建对象的时候，首先将在堆上为Dog对象分配足够的存储空间

4）这块存储空间会被清零，这将自动地将Dog对象中的所有基本类型都设置为默认值（对数字来说就是0，对布尔型和字符型也相同），而引用则被设置为null

5）执行所有出现于字段定义处的初始化动作

6）执行构造器

## 显示的静态初始化
   
> Java允许将多个静态初始化组织成一个特殊“静态子句”（有时也叫做“静态块”）
> 
> 与其他静态初始化动作一样，这段代码仅执行一次：当首次生成这个类的一个对象时，或者首次访问属于那个类的静态数据成员时（即使从未创建那个类的对象）

```java
public class Spoon{
    static int i;
    static {
        i = 47;
    }
}
```

## 非静态实例初始化

> Java中也有被称为初始化的类似语法，用来初始化每一个对象的非静态变量。
  
```java
class Mug{
    Mug(int m){
        System.out.println("Mug " + m);
    }
    void f(int m){
        System.out.println("f " + m);
    }
}
class Mugs{
    Mug mug1;
    Mug mug2;
    {
        mug1 = new Mug(1);
        mug2 = new Mug(2);
        System.out.println("Mug1 & Mug2 initialized");
    }
    Mugs(){
        System.out.println("Mugs");
    }
    Mugs(int i){
        System.out.println("Mugs(int)");
    }
    public static void main(String[] args) {
        System.out.println("Inside main()");
        new Mugs();
        System.out.println("new Mugs() completed");
        new Mugs(1);
        System.out.println("new Mugs(1) completed");
    }
}
// Output
// Inside main()
// Mug 1
// Mug 2
// Mug1 & Mug2 initialized
// Mugs
// new Mugs() completed
// Mug 1
// Mug 2
// Mug1 & Mug2 initialized
// Mugs(int)
// new Mugs(1) completed
```
上面的代码看起来它与静态初始化子句一摸一样，只是少了static关键字。这种语法对于支持“匿名内部类”的初始化是必须的，但是它也使得你可以保证无论调用了哪个显式构造器，某些操作都会发生。从输出可以看到实例化子句是在两个构造器之前执行的

## 数组初始化

> 数组只是相同类型的、同一标识符名称封装到一起的一个对象序列或基本类型数据序列。
> 
> 数组是通过方括号下标操作符[]来定义和使用的。 要定义一个数组，只需在类型名后加上一对空方括号即可int[] a1，方括号也可以置于标识符后面int a1[]

> 编译器不允许指定数组的大小。现在拥有的只是对数据的引用(已经为该引用分配了足够的存储空间)，而且也没给数组对象本身分配任何空间。为了给数组创建相应的存储空间，必须写初始化表达式。

### 数组的三种初始化方式

```
// 第一种，必须在创建数组的地方出现，由一对花括号括起来的值组成的
// 这种情况下，存储空间的分配(等价于使用new)将由编译器负责
// 初始化列表的最后一个逗号是可选的
int[] a1 = {1,2,3,4,5};
```

```
// 第二种，使用new并定义数组的长度
// 数组中元素的基本类型值会自动初始化成空值(对于数组和字符，就是0，对于布尔型，是false)
// 对于这种情况，初始化动作可以出现在代码的任何地方
int[] a1 = new int[20];
```

```
// 第三种
int[] a1 = new int[]{1,2,3,4,5};
```

### 将一个数组赋值给另一个数组
```
//  这里a2得到了关于a1的一个引用
// 此时修改a2，a1也可以看到
int[] a1 = {1,2,3,4,5};
a2 = a1;
```
### 获得数组内包含了多少个元素

```
int[] a1 = {1,2,3,4,5};
a1.length; //数组的长度
a1.length - 1; // 数组最大下标数length-1，如果访问超过的下标边界，Java会出现运行时错误
```

### 创建非基本类型的数组

```
// 创建一个非基本类型的数组，那么就是创建了一个引用数组
Integer[] a = new Integer[10];
a[i] = new Integer(1); // 创建引用数组，即使使用new的方式，也还只是一个引用数组，并且直到通过创建新的Integer对象，并把对象赋值给引用，初始化进程才算结束，如果忘记了创建对象并且试图使用数组中的空引用，就会在运行时产生异常
```

## 可变参数列表

由于所有的类都直接或间接继承于Object类，所以可以创建以Object数组为参数方法，以此获取可变参数列表

```java
//  JavaSE5之前
class A{}
public class VarArgs{
  static void printArray(Object[] args){
      for(Object obj : args){
        System.out.println(obj + "");
    }
    System.out.println();
  }

public static void main(String[] args){
      printArray(new Object[]{new Integer(47),new Float(3.14),new Double(11.11)});
      printArray(new Object[]{"one","two","three"});
      printArray(new Object[]{new A(),new A(),new A()});
  }
}
```

> JavaSE5增加的新特性，可以使用它们来定义可变参数列表
> 
> 有了可变参数，就不用显式地编写数组语法了，当你指定参数时，编译器实际上会为你去填充数组。
> 此时仍旧是一个数组。但是，这不仅仅只是从元素列表到数组的自动转换，`printArray((Object [])new Integer[]{1,2,3,4,5});`
> 中Integer数组（通过使用自动包装而创建）被转型为一个Object数组，并且传递给printArray()
> 由于此时它已经是个数组了，所以不会对它执行任何转换。
>
> 因此，如果有一组事物，可以把它们当作列表传递，而如果已经有了一个数组，该方法可以把
> 它们当作可变参数列表来接受

- 传递0个参数

```java
public class OptionalTrailingArguments{
    static void f(int required,String... trailing){ // 可变参数列表可以使用任何类型的参数，包括基本类型
        System.out.println("required: " + required + " ");
        for(String s : trailing){
            System.out.println(s + " ");
      }
      System.out.println();
  }

    public static void main(String[] args){
        f(1,"one");
        f(2,"two","three");
        f(1);
    }
}
```

> 可变参数列表可以使用除Object之外类型的任何类型的参数，包括基本类型。
 
```java
public class VarargType{
    static void f(Character... args){
         System.out.print(args.getClass);
         System.out.println(" length " + args.length);
    }

    static void g(int... args){
         System.out.print(args.getClass); 
         System.out.println(" length " + args.length);
    }
    
    public static void main(String[] args){
        f('a');
        f(); // 如果在列表中没有任何元素，那么转变成的数据的尺寸为0
        g(1);
        g();
        System.out.println("int[]: " + new int[0].getClass());
    }
}
```

```
// 运行结果
class [Ljava.lang.Character; length 1
class [Ljava.lang.Character; length 0
class [I length 1
class [I length 0
int[]: class [I
```

在上面的例子中，getClass()方法属于Object的一部分，它将产生对象的类，并且在打印该类时，可以看到表示
该类类型编码的字符串，前面的"[" 表示这是一个后面紧随类型的数组，而紧随的“I”表示类型为int

这样也验证了使用可变参数列表不依赖自动包装类，而实际上使用的是基本类型

> 可以在单一的参数列表中将类型混合在一起，而自动包装机制将有选择地将int参数提升为Integer
> 上面的情况建立在方法接收的参数类型是Interger，如果是int类型，会将Integer转为int

```java

public class AutoboxingVarargs{
    public static void f(Integer... args){
        System.out.println(args.getClass());
        for(Integer s : args){
            System.out.print(s + " ");
        }
        System.out.println();
    }

    public static void g(int... args){
        System.out.println(args.getClass());
        for(Integer s : args){
            System.out.print(s + " ");
        }
        System.out.println();
    }

    public static void main(String[] args){
        f(new Integer(1),new Integer(2));
        f(4,5,6,7,8,9);
        f(10,new Integer(11),12);// 可以在单一的参数列表中将类型混合在一起，而自动包装机制将有选择地将int参数提升为Integer
        System.out.println("============");
        g(10,new Integer(11),12);
    }
}
```

可变参数列表使得重载过程变得复杂了，下面的例子中，编译器都会使用自动包装机制来匹配重载的方法，然后调用最明确匹配的方法，但是在不使用参数调用f()时，编译器就无法直到应该调用哪一个方法了。可以给所有方法增加一个非可变参数，但是建议的是 只在重载方法的一个版本上使用可变参数列表，或者压根不用它

```java
public class OverloadingVarargs{
    static void f(Character... args){
          for(Character c : args){
            System.out.print(c + " ");
          }
          System.out.println();
    }

    static void f(Integer... args){
          for(Integer c : args){
            System.out.print(i + " ");
          }
          System.out.println();
    }

    static void f(Long... args){
          System.out.println("third");
    }

    public static void main(String[] args){
        f(a,b,c);
        f(1);
        f(2,1);
        f(0);
        f(0L);
        // f(); // 无法调用
    }
}
```

## 枚举类型

> 枚举类的语法：由于枚举类型的实例是常量，因此按照命名惯例它们都用大写字母表示（如果一个名字中
> 有多个单词，用下划线将它们隔开）

```java
/**
* 这里创建了一个名为Spiciness的枚举类型，它具有5个具名值
*/
public enum Spiciness{
    NOT,MILD,MEDIUM,HOT,FLAMING
}
```

> 为了使用enum，需要创建一个该类型的引用，并将其赋值给某个实例：

```java
public class SimpleEnumUse{
    public static void main(String[] args){
        Spiciness howHot = Spiciness.MEDIUM;
        System.out.println(howHot);
    }
}
```

> 在创建enum时，编译器会自动添加一些有用的特性：
> 
> 1）toString() 以便很方便地显示某个enum实例的名字，这正是上面的打印语句如何产生其输出的答案
>
> 2）ordinal() 用来表示某个特定enum常量的声明顺序
>
> 3）static values() 用来按照enum常量的声明顺序，产生由这些常量值构成的数组

```java
public class EnumOrder{
    public static void main(String[] args){
      for(Spiciness s: Spiciness.values()){
          System.out.println(s + ", ordinal " + s.ordinal());
        }
    }
}
```

由于switch是要在有限的集合中进行选择，enum可以在switch语句中使用

```java
public class Burrito{
    Spiciness degree;
    public Burrito(Spiciness degree){
        this.degree = degree;
    }

    public void describe(){
        System.out.println("this burrito is");
        switch (degree){
            case NOT: System.out.println("not spicy at all");break;
            case MILD:
            case MEDIUM:System.out.println("a little hot");break;
            case HOT:
            case FLAMING:
            default: System.out.println("maybe too hot.");
        }
    }
    public static void main(String[] args){
        Burrito plain = new Burrito(Spiciness.NOT);
        Burrito greenChile = new Burrito(Spiciness.MEDIUM);
        Burrito jalaeno = new Burrito(Spiciness.HOT);
        plain.describe();
        greenChile.describe();
        jalaeno.describe();
    }
}
```

所以，大体上，你可以将enum用作另外一个创建数据类型的方式，然后直接将所得到的类型拿来使用，这正是关键所在。

## 抽象类和抽象方法

> 建立通用接口的目的是：使子类继承从而不同的子类可以用不同的方式表示此接口。通用接口建立起一种基本的形式，以此表示所有子类的共同部门。可以称
> 这样的类为抽象类，创建抽象类是希望通过这个接通用接口操纵一系列。

> 定义抽象方法，仅有声明而没有方法体，比如abstract void f();，包含抽象方法的类叫做抽象类。如果一个类包含一个或多个抽象方法，该类必须被限定为抽象的

抽象类不能初始化对象，否则会报编译器错误，如果从一个抽象类继承，并创建子类的对象。子类在创建时必须实现抽象类提供的方法定义。如果不这么做，那么子类也是
抽象类，编译器会强制要求用abstract关键字来限定这个类。

可以创建一个没有任何抽象方法的抽象类，因为除了可以只提供声明的抽象方法外，还可以包括普通方法。这种类的作用是阻止产生这个类的任何对象

![](https://upload-images.jianshu.io/upload_images/2765653-7d1dd12d4434c1c4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```java
abstract class Instrument{
    private int i;
    public abstract void play(Note n);
    public String what(){
        return "Instrument";
    }
    public abstract void adjust();
}

class Wind extends Instrument{
    @Override
    public void play(Note n) {
        System.out.println("Wind.play()" + n);
    }

    public String what(){
        return "Wind";
    }
    public void adjust(){}
}

class Percussion extends Instrument{
    @Override
    public void play(Note n) {
        System.out.println("Percussion.play()" + n);
    }
    public String what(){
        return "Percussion";
    }
    public void adjust(){}
}

class Stringed extends Instrument{
    @Override
    public void play(Note n) {
        System.out.println("Stringed.play()" + n);
    }
    public String what(){
        return "Stringed";
    }
    public void adjust(){}
}

class Brass extends Wind{
    public void play(Note n) {
        System.out.println("Brass.play()" + n);
    }
    public String what(){
        return "Brass";
    }
}

class Woodwind extends Wind{
    public void play(Note n) {
        System.out.println("Woodwind.play()" + n);
    }
    public String what(){
        return "Woodwind";
    }
}

public class Music4 {

    static void tune(Instrument i){
        i.play(Note.MIDDLE_C);
    }
    static void tuneAll(Instrument[] e){
        for(Instrument i : e){
            tune(i);
        }
    }
    public static void main(String[] args) {
        Instrument[] orchestra = {
                new Wind(),
                new Percussion(),
                new Stringed(),
                new Brass(),
                new Woodwind()
        };
        tuneAll(orchestra);
    }
}
```

## 接口

> interface关键字产生一个完全抽象的类，方法不提供任何具体实现。它允许创建者确定方法名、参数列表、返回类型，
> 但是没有任何方法实现。接口只提供了形式，而未提供任何具体实现

创建接口类，需要interface关键字来替代class关键字。可以在interface关键字前面添加public关键字（但仅限于
该接口在其同名的文件中被定义）。如果不添加public关键字，则它只具有包访问权限，这样它就只能在同一个包内可用。在接口中可以显式地将方法
声明为public的。

如果接口声明为pulic的，在接口中可以显式地将方法声明为public的，但即使不这么做，它们也是public的。接口也可以包含域，
但是这些域隐式是static和final的

> 一个类实现某个特定接口（或者是一组接口），需要使用implements关键字，一个类实现了某个接口后，这个类就成为一个普通的类，就可以用常规的方式使用继承这个类的方法或扩展这个类的方法

![](https://upload-images.jianshu.io/upload_images/2765653-1883a22d3cc4fd19.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```java
interface Instrument{
     int VALUE = 5;
     void play(Note n);
     abstract void adjust();
}

class Wind implements Instrument{
    public void play(Note n) {
        System.out.println(this + ".play()" + n);
    }

    @Override
    public String toString() {
        return "Wind";
    }

    public void adjust(){}
}

class Percussion implements Instrument{
    public void play(Note n) {
        System.out.println(this + ".play()" + n);
    }
    @Override
    public String toString() {
        return "Percussion";
    }

    public void adjust(){}
}

class Stringed implements Instrument{
    public void play(Note n) {
        System.out.println(this + ".play()" + n);
    }
    @Override
    public String toString() {
        return "PercusStringedsion";
    }

    public void adjust(){}
}

class Brass extends Wind{
    @Override
    public String toString() {
        return "Brass";
    }
}

class Woodwind extends Wind{
    @Override
    public String toString() {
        return "Woodwind";
    }
}

public class Music5 {

    static void tune(Instrument i){
        i.play(Note.MIDDLE_C);
    }
    static void tuneAll(Instrument[] e){
        for(Instrument i : e){
            tune(i);
        }
    }
    public static void main(String[] args) {
        Instrument[] orchestra = {
                new Wind(),
                new Percussion(),
                new Stringed(),
                new Brass(),
                new Woodwind()
        };
        tuneAll(orchestra);
    }
}
```
### 完全解耦

```java
class Processor{
    public String name(){
        return getClass().getSimpleName();
    }

    Object process(Object input){
        return input;
    }
}

class Upcase extends Processor{
    String process(Object input){
        return ((String)input).toUpperCase();
    }
}

class Downcase extends Processor{
    String process(Object input){
        return ((String)input).toLowerCase();
    }
}

class Splitter extends Processor{
    String process(Object input){
        return Arrays.toString(((String)input).split(" "));
    }
}

public class Apply {
    public static void process(Processor p,Object s){
        System.out.println("Using Processor " + p.name());
        System.out.println(p.process(s));
    }

    public static String s = "Disagreement with beliefs is by definition incorrect";

    public static void main(String[] args) {
        process(new Upcase(),s);
        process(new Downcase(),s);
        process(new Splitter(),s);
    }
}
```

上面的例子中：Apply.process()方法接受任何类型的Processor，并将接受的额Object对象s传递给Processor的process方法
处理，然后打印结果。

> 这样创建一个能够根据所传递的参数对象的不同而具有不同行为的方法，被称为策略设计模式。


这类方法包含所要执行的算法中固定不变的部分，而策略包含变化的部分。

策略就是传递进去的参数对象，它包含要执行的代码。这里，Processor对象就是一个策略，在main()方法中可以看到有三种不同类型的策略应用到了String类型的s对象上

spilt()方法是String类的一部分，它接受String类型的对象，并以传递进来的参数作为边界，将String对象分隔开，然后返回一个数组[]。它在这里被用来当作创建String数组的快捷方式

### Java中的多重继承

> 子类继承非接口和多个接口：class A extends B implements Inter1,Inter2,Inter3{}

```java
interface CanFight{
    void fight();
}

interface CanSwim{
    void swim();
}

interface CanFly{
    void fly();
}

class ActionCharacter{
    public void fight(){}
}

class Hero extends ActionCharacter implements CanFight,CanSwim,CanFly{
    public void swim(){}
    public void fly(){}
}
public class Adventure {
    public static void t(CanFight x){
        x.fight();
    }
    
    public static void u(CanSwim x){
        x.swim();
    }
    
    public static void v(CanFly x){
        x.fly();
    }
    
    public static void w(ActionCharacter x){
        x.fight();
    }
    
    public static void main(String[] args){
        Hero h = new Hero();
        t(h);
        u(h);
        v(h);
        w(h);
    }
}
```

Hero组合了具体类ActionCharacter和接口CanFight、CanSwim、CanFly。当通过这种方式将一个具体类和多个接口组合到一起时，具体类必须放在前面，后面跟着的才是接口。Hero中没有显式地提供fight()的定义，由于在父类ActionCharacter存在fight()的定义，

### 通过继承来扩展接口

> 通过继承，可以很容易地在接口中添加新的方法声明，还可以通过继承在新接口中组合数个接口。这两种情况都可以获得新的接口

```java
interface Monster{
    void manace(); 
}
interface DangerousMonster extends Monster{  // 通过继承在新接口中添加新的方法声明
    void destory(); 
}
interface Lethal{
    void kill(); 
}

class DragonZilla implements DangerousMonster{

    @Override
    public void manace() {}

    @Override
    public void destory() {}
}
interface Vampire extends DangerousMonster,Lethal{ // 通过继承在新接口中组合数个接口
    void drinkBlood();
}

class VeryBadVampire implements Vampire{
    @Override
    public void manace() {
        
    }
    @Override
    public void destory() {

    }
    @Override
    public void kill() {

    }
    @Override
    public void drinkBlood() {

    }
}
public class HarrorShow {
}
```

### 适配接口

接口最吸引人的原因之一就是允许同一个接口具有多个不同的具体实现。它的体现形式通常是一个接受接口类型的方法，而该接口的实现和向该方法传递的对象则取决于方法的使用者。因此接口的一种常见用法就是 策略设计模式，编写一个执行某些操作的方法，而该方法接受一个同样是你指定的接口。

### 接口中的域

因为放入接口中的任何域都自动是statice和final的，所以接口成为了一种很便捷的用来常见常量组的工具。Java中标识具有常量初始化值的static final时，会使用大写字母的风格（标识符中用下划线来分隔多个单词）。接口中的域自动是public。但JavaSE5后，可以使用更加强大而灵活的enum关键字。

在接口中定义的域不能是“空final”，大师可以被非常量表达式初始化。

```java
public interface RandVals {
    Random RAND = new Random(47);
    int RANDOM_INT = RAND.nextInt(10);
    long RANDOM_LONG = RAND.nextLong() * 10;
    float RANDOM_FLOAT = RAND.nextFloat() * 10;
    double RANDOM_DOUBLE = RAND.nextDouble() * 10;
}
```

域是static的，它们就可以在类第一次加载时被初始化，这发生在任何域首次被访问。并且这些域并不是接口的一部分，它们的值被存储在该接口的静态存储区域内

```java
public class TestRandVals {
    public static void main(String[] args) {
        System.out.println(RandVals.RANDOM_INT);
        System.out.println(RandVals.RANDOM_LONG);
        System.out.println(RandVals.RANDOM_FLOAT);
        System.out.println(RandVals.RANDOM_DOUBLE);
    }
}
```

###  接口与工厂

生成遵循某个接口的对象的典型方式就是工厂方法设计模式，在工厂对象上调用的是创建方法，而该工厂对象将生成接口的某个实现的对象。理论上，通过这种方式，我们的代码将完全与接口的实现分离，这就使得我们可以透明地将某个实现替换为另一个实现。

```java
interface Service{
    void method1();
    void method2();
}

class Implementalion1 implements Service{
    Implementalion1(){}

    @Override
    public void method1() {
        System.out.println("Implementalion1 method1");
    }

    @Override
    public void method2() {
        System.out.println("Implementalion1 method2");
    }
}

class Implementalion2 implements Service{
    Implementalion2(){}

    @Override
    public void method1() {
        System.out.println("Implementalion2 method1");
    }

    @Override
    public void method2() {
        System.out.println("Implementalion2 method2");
    }
}

interface ServiceFactory{
    Service getService();
}

class Implementation1Factory implements ServiceFactory{
    public Service getService(){
        return new Implementalion1();
    }

}

class Implementation2Factory implements ServiceFactory{
    public Service getService(){
        return new Implementalion2();
    }

}
public class Factories {
    
    public static void serviceConsumer(ServiceFactory fact){
        Service s = fact.getService();
        s.method1();
        s.method2();
    }
    public static void main(String[] args) {
        serviceConsumer(new Implementation1Factory());
        serviceConsumer(new Implementation2Factory());
    }
}
```

## 内部类

> 将一个类的定义放在另一个类的定义内部，这就是内部类

###  创建内部类

> 创建内部类的方式：把类的定义置于外围类的里面

```java
public class Parcel1 {
    class Contents{
        private int i = 11;
        public int value(){
            return i;
        }
    }

    class Destination{
        private String label;
        Destination(String whereTo){
            label = whereTo;
        }

        String readLabel(){
            return label;
        }
    }

    public void ship(String dest){
        Contents c = new Contents();
        Destination d = new Destination(dest);
        System.out.println(d.readLabel());
    }

    public static void main(String[] args) {
        Parcel1 p = new Parcel1();
        p.ship("Tasmania");
    }
}
```

> 更典型的情况是，外部类将有一个方法，该方法返回一个指向内部类的引用
  
```java
public class Parcel2 {
    class Contents{
        private int i = 11;
        public int value(){
            return i;
        }
    }

    class Destination{
        private String label;
        Destination(String whereTo){
            label = whereTo;
        }

        String readLabel(){
            return label;
        }
    }
    
    public Destination to(String s){
        return new Destination(s);
    }
    
    public Contents contents(){
        return new Contents();
    }
    
    public void ship(String dest){
        Contents c = contents();
        Destination d = to(dest);
        System.out.println(d.readLabel());
    }

    public static void main(String[] args) {
        Parcel2 p = new Parcel2();
        p.ship("Tasmania");
        Parcel2 q = new Parcel2();
        Parcel2.Contents c = q.contents();
        Parcel2.Destination d = q.to("Borneo");
    }
}
```
如果想从外部类的非静态方法之外的任意位置创建某个内部类的对象（在静态方法内部创建某个内部类的对象），那么必须像在main()方法中那样，具体地指明这个对象的类型：OuterClassName.InnerClassName

### 链接到外部类

> 当生成一个内部类的对象时，此对象与它的外部类对象之间产生了一种练习，所以它能访问其外围对象的所有成员，而不需要任何特殊条件

```java
interface Selector{
    boolean end();
    Object current();
    void next();
}
public class Sequence {
    private Object[] items;
    private int next = 0;
    public Sequence(int size) {
        items = new Object[size];
    }
    public void add(Object x){
        if(next < items.length){
            items[next++] = x;
        }
    }
    private class SequenceSelector implements Selector{
        private int i = 0;
        public boolean end(){
            return i == items.length;
        }
        public Object current(){
            return items[i];
        }

        public void next(){
            if(i < items.length){
                i++;
            }
        }
    }

    public Selector selector(){
        return new SequenceSelector();
    }

    public static void main(String[] args) {
        Sequence sequence = new Sequence(10);
        for(int i = 0; i <10;i++){
            sequence.add(Integer.toString(i));
        }
        Selector selector = sequence.selector();
        while (!selector.end()){
            System.out.println(selector.current() + " ");
            selector.next();
        }
    }
}
```

Sequence类只是一个固定大小的Object数组，以类的形式包装了起来。可以调用add()在序列末增加新的Object（只要还有空间）。要获取Sequence中的每一个对象，可以使用Selector接口。这是“迭代器”设计模式的一个例子。

Selector允许你检查序列是否到末尾了end()，访问当前对象current()，以及移到序列中的下一个对象next()。因为Selector是一个接口，所以别的类可以按他们自己的方式来实现这个接口，并且别的方法能以此接口为参数，来生成更加通用的代码。

SequenceSelector类中的方法end()、current()、next()都用到了objects，这是一个引用，它不是SequenceSelector的一部分，而是外围类中的private字段。然而内部类访问外部类的方法和字段，就像自己拥有他们一样。

所以内部类自动拥有对其外部类所有成员的访问权。这是如何做到的呢？当某个外围类的对象创建了一个内部类对象时，此内部类对象必定会秘密的捕获一个指向那个外围类对象的引用。然后，在你访问此外围类的成员时，就是用那个引用来选择外围类的成员。

还要注意的是：内部类的对象只能在其与外部类的对象相关联的情况下才能创建（在内部类是非static类时）

### 使用.this与.new

> 如果生成对外部类对象的引用，可以使用外部类的名字后面紧跟着圆点和this。
  
```java
public class DotThis {
    
    void f(){
        System.out.println("DotThis.f()");
    }
    
    public class Inner{
        public DotThis outer(){
            return DotThis.this;
        }
    }
    
    public Inner inner(){
        return new Inner();
    }

    public static void main(String[] args) {
        DotThis dt = new DotThis();
        DotThis.Inner dti = dt.inner();
        dti.outer().f();
    }
}
```

通过外部类对象创建其内部类的对象。必须在new表达式中提供对其外部类对象的引用。需要使用.new语法：

```java
public class DotNew {
    public class Inner{}
    public static void main(String[] args){
        DotNew dn = new DotNew();
        DotNew.Inner dni = dn.new Inner();
    }
}
```

但如果创建的是静态内部类，那么就不需要对外部类对象的引用

### 内部类与向上转型

内部类是某个接口的实现，这个实现能够完全不可见，并且不可用。使用时只得到指向父类或接口的引用，所以能够很方便的隐藏实现细节

```java
public interface Destination { // 表示对外可用的接口，其实现在内部类
    String readLabel();
}
```

```java
public interface Contents {  // 表示对外可用的接口，其实现在内部类
    int value();
}
```

```java
class Parcel4{
    private class PContents implements Contents{ // 内部类实现接口Contents
        private int i = 11;
        public int value(){
            return i;
        }
    }

    protected class PDestination implements Destination{ // 内部类实现接口Destination
        private String label;
        private PDestination(String whereTo){
            label = whereTo;
        }
        public String readLabel(){
            return label;
        }
    }

    public Destination destination(String s){
        return new PDestination(s);
    }

    public Contents contents(){
        return new PContents();
    }
}
public class TestParcel {
    public static void main(String[] args) {
        Parcel4 p = new Parcel4();
        Contents c = p.contents(); // 创建内部类PContents的对象，指向接口的引用Contents
        Destination d = p.destination("Tasmania");  // 创建内部类PDestination的对象，指向接口的引用Destination
        // Parcel4.PContents pc = p.new PContens(); // 不能直接创建内部类因为，PContents是私有的
    }
}
```

### 在方法和作用域内的内部类

可以在一个方法里面或者任意的作用域内定义内部类。这样做的原因是：

1）实现某类型的接口，于是创建并返回对其的引用

2）要解决一个复杂问题，通过创建一个类来辅助解决，但是又不希望这个类是公共可用的

除了在类中定义内部类，还可以实现：

1）定义在方法中的类

2）定义在作用域内的类，此作用域在方法的内部

3）实现了接口的匿名类

4）匿名类，扩展了非默认构造器的类

5）匿名类，执行字段初始化

6）匿名类，通过实例初始化实现构造（匿名类不可能有构造器）

第一例子展示定义在方法中的类，这被称作局部内部类

```java
public interface Destination {
    String readLabel();
}
```

```java
public class Parcel5 {
    public Destination destination(String s){
        class PDestination implements Destination{
            private String label;
            private PDestination(String whereTo){
                label = whereTo;
            }
            public String readLabel(){
                return label;
            }
        }

        return new PDestination(s);
    }

    public static void main(String[] args) {
        Parcel5 p = new Parcel5();
        Destination d = p.destination("Tasmania");
    }
}
```

PDestination类是destination()方法的一部分，而不是Parcel5的一部分。所以，在destination()之外不能访问PDestination。注意出现在return语句中的向上转型--返回的是Destination的引用，它是PDestination的父类。虽然在destination()方法中定义了内部类PDestination，但并不意味着一旦destination()方法执行完毕，PDestination就不可用了

### 匿名内部类

```java
public interface Contents {
    int value();
}
```

```java
public class Parcel7 {
    public Contents contents(){
        return new Contents() {
            private int i = 11;
            @Override
            public int value() {
                return i;
            }
        };
    }

    public static void main(String[] args) {
        Parcel7 p = new Parcel7();
        Contents c = p.contents();
    }
}
```

contents()方法将返回值的生成与表示这个返回值的类的定义结合在一起。并且这个类匿名的，没有名字。

在上面的匿名内部类中，使用了默认的构造器来生成Contents，下面的代码展示的是，如果父类需要一个有参数的构造器，应该怎么办？

```java
public class Parcel8 {
    public Wrapping wrapping(int x){
        return new Wrapping(x){
            public int value(){
                return super.value() * 47;
            }
        };
    }
    public static void main(String[] args){
        Parcel8 p = new Parcel8();
        Wrapping w = p.wrapping(10);
        System.out.println(w.value());
    }
}
```

```java
public class Wrapping {
    int i ;
    public Wrapping(int i){
        this.i = i;
    }

    public int value(){
        return i;
    }
}
```

只需简单地传递合适的参数给父类的构造器即可，这里是将x传进new Wrapping(x)。在匿名内部类末尾的分毫，并不是用来标记此内部类结束的。实际上，它标记的是表达式的结束。只不过这个表达式正好包含了匿名内部类而已。这与别的地方使用的分号是一致的

在匿名内部类中定义字段时，还能够对其执行初始化操作：

```java
public class Parcel9 {
    public Destination destination(final String dest){
        return new Destination() {
            private String label = dest;
            @Override
            public String readLabel() {
                return label;
            }
        };
    }

    public static void main(String[] args) {
        Parcel9 p = new Parcel9();
        Destination d = p.destination("Tasmania");
    }
}
```

```java
public interface Destination {
    String readLabel();
}
```

如果定义一个匿名内部类，并且希望它使用一个在其外部定义的对象，那么编译器会要求其参数引用是final的，就像你在destination()的参数中看到的那样，如果忘记了，会得到一个编译时错误。

通过实例初始化，能够达到为匿名内部类创建一个构造器的效果：

```java
abstract class Base{
    public Base(int i){
        System.out.println("Base constructor,i = " + i);
    }

    public abstract void f();
}
public class AnonymousConstructor {
    public static Base getBase(int i){
        return new Base(i) {
            {
                System.out.println("Inside instance initializer");
            }
            @Override
            public void f() {
                System.out.println("In anonymous f()");
            }
        };
    }

    public static void main(String[] args) {
        Base base = getBase(47);
        base.f();
    }
}
```

在上面的例子中，不要求变量i一定是final，因为i被传递给匿名类的基类的构造器，它并不会在匿名类内部被直接使用

### 嵌套类

如果不需要内部类对象与其外部类对象之间有联系，可以将内部类声明为static，这称为“嵌套类”，普通内部类与嵌套类的区别：普通的内部类对象隐式地保存了一个引用，指向创建它的外部类。然后，内部类是static的时，就不会这样了，嵌套类意味着：

1）要创建嵌套类的对象，并不需要其外部类的对象

2）不能从嵌套类的对象中访问其非静态的外部类对象

嵌套类和普通内部类还有一个区别。普通内部类的字段与方法，普通的内部类不能有static数据和static字段，也不能包含嵌套类。但是嵌套类可以包含这些东西。

```java
public class Parcel11 {
    
    private static class ParcelContents implements Contents{
        private int i = 11;
        public int value(){
            return i;
        }
    }
    
    protected static class ParcelDestination implements Destination{
        private String label;
        private ParcelDestination(String whereTo){
            label = whereTo;
        }
        
        public String readLabel(){
            return label;
        }
        
        public static void f(){}
        static int x = 10;
        static class AnotherLevel{
            public static void f(){}
            static int x = 10;
        }
    }
    
    public static Destination destination(String s){
        return new ParcelDestination(s);
    }
    
    public static Contents contents(){
        return new ParcelContents();
    }

    public static void main(String[] args) {
        Contents c = contents();
        Destination d = destination("Tasmania");
    }
}
```

### 内部类的继承

```java
class WithInner{
    class Inner{}
}
public class InheritInner extends WithInner.Inner {
    InheritInner(WithInner wi){
        wi.super();
    }

    public static void main(String[] args) {
        WithInner wi = new WithInner();
        InheritInner ii = new InheritInner(wi);
    }
}
```

从上面的例子中可以看出，当继承了某个外部类的时候，内部类并没有发生什么特别神奇的变化。这两个内部类是完全独立的两个实体，各自在自己的命名空间内，当然，明确地继承某个内部类也是可以的：

```java
class Egg2{
    protected class Yolk{
        public Yolk(){
            System.out.println("Egg2.Yolk()");
        }
        public void f(){
            System.out.println("Egg2.Yolk.f()");
        }
    }

    private Yolk y = new Yolk();
    public Egg2(){
        System.out.println("New Egg2()");
    }

    public void insertYolk(Yolk yy){
        y = yy;
    }

    public void g(){
        y.f();
    }
}
public class BigEgg2 extends Egg2{
    public class Yolk extends Egg2.Yolk{
        public Yolk(){
            System.out.println("BigEgg2.Yolk()");
        }
        public void f(){
            System.out.println("BigEgg2.Yolk.f()");
        }
    }

    public BigEgg2(){
        insertYolk(new Yolk());
    }

    public static void main(String[] args) {
        Egg2 e2 = new BigEgg2();
        e2.g();
    }
}
```

BigEgg2.Yokl通过extends Egg2.Yolk 明确地继承了此内部类，并且覆盖了其中地方法。

### 局部内部类

可以在代码块里创建内部类，典型的方式是在一个方法体地里面创建。局部内部类不能有访问说明符，因为它不是外部类的一部分；但是它可以访问当前代码块内的常量，以及此外部类的所有成员。下面的例子对局部内部类与匿名内部类的创建进行了比较：

```java
interface Counter{
    int next();
}
public class LocalInnerClass {
    private int count = 0;
    Counter getCounter(final String name){
        class LocalCounter implements Counter{
            public LocalCounter(){
                System.out.println("LocalCounter");
            }
            public int next(){
                System.out.println(name);
                return count++;
            }
        }
        return new LocalCounter();
    }

    Counter getCounter2(final String name){
        return new Counter() {
            {
                System.out.println("Counter()");
            }
            @Override
            public int next() {
                System.out.println(name);
                return count++;
            }
        };
    }

    public static void main(String[] args) {
        LocalInnerClass lic = new LocalInnerClass();
        Counter c1 = lic.getCounter("Local inner");
        Counter c2 = lic.getCounter2("Anonymous inner");
        for(int i = 0;i < 5; i++){
            System.out.println(c1.next());
        }
        for(int i = 0; i < 5;i++){
            System.out.println(c2.next());
        }
    }
}
```

### 内部类标识符

由于每个类在编译后产生一个.class文件，其中包含了如果创建该类型的对象的全部信息。（此信息产生一个“meta-class”，叫做Class对象）。内部类也必须生成一个.class文件以包含它们的Class对象信息。这些类文件的命名有严格的规则：外部类的名字，加上“$”，再加上内部类的名字。例如，LocalInnerClass.java生成的.class文件包括：

```
Counter.class // interface Counter{}
LocalInnerClass$1.class // 如果内部类是匿名的，编译器会简单地产生一个数字作为其标识符
LocalInnerClass$1LocalCounter.class // 局部内部类
LocalInnerClass.class // class LocalInnerClass{}
```

## 字符串

### 1. 不可变String

String是不可变的，String类中每一个看起来会修改String值的方法，实际上都是创建了一个全新的String对象，以包含修改后的字符串内容。而最初的String对象则丝毫未动

 ```
public class Immutable {
    public static String upcase(String s){
        return s.toUpperCase();
    }

    public static void main(String[] args) {
        String q = "howdy";
        System.out.println(q);
        String qq = upcase(q);
        System.out.println(qq);
        System.out.println(q);
    }
}
``` 
当把q传给upcase()方法时，实际传递的是引用的一个拷贝。其实，每当把String对象作为方法的参数时，都会复制一份引用，而该引用所指的对象其实一直待在单一的物理位置上，从未动过。

回到upcase()的定义，传入其中的引用有了名字s，只有upcase()运行的时候，局部引用s才存在。一旦upcase()运行结束，s就消失了。当然了，upcase()的返回值，其实只是最终结果的引用。这足以说明，upcase()返回的引用已经指向了一个新的对象，而原本的q则还在原地

### 2. 重载“+” 和StringBuilder

重载的意思是，一个操作符在引用于特定的类时，被赋予了特殊的意义（用于String的“+”与“+=”是Java中仅有的两个重载过的操作符，而Java并不允许成员重载任何操作符）

操作符“+”可以用来连接String：

```
public class Contatenation {
    public static void main(String[] args) {
        String mango = "mango";
        String s = "abc" + mango + "def" + 47;
        System.out.println(s);
    }
}
```

```
public class UsingStringBuilder {
    public static Random rand = new Random(47);
    public String toString(){
        StringBuilder result = new StringBuilder("[");
        for(int i = 0; i < 25;i++){
            result.append(rand.nextInt(100));
            result.append(", ");
        }

        result.delete(result.length()-2,result.length());
        result.append("]");
        return result.toString();
    }

    public static void main(String[] args) {
        UsingStringBuilder usb = new UsingStringBuilder();
        System.out.println(usb);
    }
}
```

StringBuilder提供了丰富而全面的方法，包括insert()、replace()、substring()甚至reverse()，但最常用的还是append()和toString()。还有delete()方法。

### 3.格式化输出

JavaSE5引入的format方法可用于PrintStream或PrintWriter对象，其中也包括System.out对象。

```
public class SimpleFormat {
    public static void main(String[] args) {
        int x = 5;
        double y = 5.332542;
        System.out.println("Row 1: [ " + x + " " + y + "]");
        System.out.format("Row 1: [%d %f]\n" ,x,y);
        System.out.printf("Row 1: [%d %f]\n" ,x,y);
    }
}
``` 
format()与printf()是等价的，它们只需要一个简单的格式化字符串，加上一串参数即可，每个参数对应一个格式化修饰符

在Java中，所有新的格式化功能都由java.util.Formatter 类处理。可以将Formatter看作一个翻译器，它将你的格式化字符串与数据翻译称需要的结果，当你创建一个Formatter对象的时候，需要向其构造器传递一些信息，告诉它最终的结果将向哪里输出

```
public class Turtle {
    private String name;
    private Formatter f;
    public Turtle(String name,Formatter f){
        this.name = name;
        this.f = f;
    }

    public void move(int x,int y){
        f.format("%s The Turtle is at (%d,%d)\n",name,x,y);
    }

    public static void main(String[] args) {
        PrintStream outAlias  = System.out;
        Turtle tommy = new Turtle("Tommy",new Formatter(System.out));
        Turtle terry = new Turtle("terry",new Formatter(outAlias));
        tommy.move(0,0);
        tommy.move(3,4);
        tommy.move(3,3);
        terry.move(4,8);
        terry.move(2,5);
        terry.move(3,3);
    }
}
```

### 4. 扫描输入

从文本或标准输入读取数据还是一件相当痛苦的事情。一般的解决之道就是读入一行文本，对其进行分词，然后使用Integer、Double等类的各种解析方法来解析数据
```
public class SimpleRead {
    public static BufferedReader input = new BufferedReader(new StringReader("Sir Robin of Camelot\n 22 1.61803"));

    public static void main(String[] args) {
        try {
            System.out.println("What is your name?");
            String name = input.readLine();
            System.out.println(name);
            System.out.println("How old are you ? what is your favorite double?");
            System.out.println("(input:<age> <double>");
            String numbers = input.readLine();
            System.out.println(numbers);
            String[] numArray = numbers.split(" ");
            int age = Integer.parseInt(numArray[0]);
            double favorite = Double.parseDouble(numArray[1]);
            System.out.format("Hi %s.\n",name);
            System.out.format("In 5 years you will be %d.\n",age+5);
            System.out.format("My favorite double is %f.",favorite/2);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
Scanner的构造器可以接受任何类型的输入对象，包括File对象、InputStream、String或者下面例子中的Readable对象。

```
public class BetterRead {
    public static void main(String[] args) {
        Scanner stdin = new Scanner(SimpleRead.input);
        System.out.println("What is your name?");

        String name = stdin.nextLine();
        System.out.println(name);
        System.out.println("How old are you ? what is your favorite double?");
        System.out.println("(input:<age> <double>");

        int age = stdin.nextInt();
        double favorite = stdin.nextDouble();
        System.out.println(age);
        System.out.println(favorite);
        System.out.format("Hi %s.\n",name);
        System.out.format("In 5 years you will be %d.\n",age+5);
        System.out.format("My favorite double is %f.",favorite/2);
    }
}
```

## 异常

Java异常是Java提供的用于处理程序中错误的一种机制。所谓错误是指在程序**运行的过程中发生的一些异常事件**（如：除0溢出，数组下标越界，所要读取的文件不存在）**并非在编写代码出现的编译时错误（注意：发生异常时，观察错误的名字和行号最重要），设计良好的程序应该在异常发生时提供处理这些错误的方法，使得程序不会因为异常的发生而阻断或产生不可遇见的结果。

Java程序的执行过程中如果出现异常事件，可以生成一个异常类对象，该异常对象封装了异常事件的信息并被提交给Java运行时系统，这个过程称为抛出（throw）异常。当Java运行时系统接收到异常对象时，会寻找能处理这一异常的代码并把当前异常对象交给其处理，这一过程称为捕获（catch）异常。

```
public class TestEx{
    public static void (String[] args){
        int[] arr = {1,2,3};
        System.out.println("arr[2]");
        try{
            System.out.println(2/0);
        }catch(ArithmeticException e){ // 捕获异常并在代码块中处理，e是为异常命名，因为生成异常的后会生成一个异常的对象
            System.out.println("出错了。。。")
            e.printStackTrace(); // 把错误的堆栈信息打出来
        }
    }
}
```

再看一个例子
```
public void someMethod() throws SomeException{ // 在方法后面定义异常，在使用时要注意此异常
    if(someCondition()){
        throw new SomeException("错误原因") // 构造并抛出异常对象
    }
}
```

#### 异常的分类


![](https://upload-images.jianshu.io/upload_images/2765653-d752ad18629e5f87.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Error：称为错误，由Java虚拟机生成并抛出，包括动态连接失败、虚拟机错误等，程序对其不做处理
Exception：所有异常类的父类，其子类对应了各种各样可能出现的异常，一般需要用户显式的声明或捕获
RuntimeException ：一类特殊的异常，如被0除，数组下标超范围等，其产生比较频繁，处理麻烦，如果显式的声明或捕获将会将会程序可读性和运行效率影响很大。因此由系统自动检测并将它们交给缺省的异常处理程序（用户可不必对其处理）
除了RuntimeException的Exception：必须catch ，在JDK里写了throw的必须的catch

```
Exception(in java.lang)
    ClassNotFoundException
    IOException
    InterruptedException
    RuntimeException
        ArithmeticException NullPointerException
        IndexOutOfBoundsException
          ArrayIndexOutObBoundsException
          StringIndexOutBoundsException
```

####异常的捕获和处理

![](https://upload-images.jianshu.io/upload_images/2765653-349e040b408bc12a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

try 语句块中有多个语句时，执行到某个语句产生异常时，此时这个try 语句块中其他的语句不再执行，直接到对应的catch语句，最后finally语句；如果代码块中有多个try语句时，一个try执行时catch到异常，另一个try还会继续执行；如果一个try语句中没有捕获异常也要走finally语句

也可以不写trycatch 直接throws在方法抛出异常，当别人调这个方法的时候处理，别人也可以选择不处理继续throws在方法抛出异常，main()方法也可以想向上抛出交给java运行时系统处理

try{...}语句指定了一段代码，该段代码就是一次捕获并处理异常的范围，在执行过程中，该段代码可能会产生并抛出一种或几种类型的异常对象。它后面的catch语句要分别对这些异常做相应的处理，如果没有的catch代码都会被略过不执行

在catch语句中时对异常进行处理的代码，每个try语句块可以伴随一个或多个catch语句，用于处理可能产生的不同类型的异常对象。在catch中声明的异常对象封装了异常事件发生的信息，在catch语句块中可以使用和这个对象一些方法获取这些信息。  

```
getMessage() 用来得到有关异常事件的信息
printStackTrace() 用来跟踪异常事件发生时执行堆栈的内容
```

finally语句为异常处理提供一个统一的出口，使得在控制流程转到程序的其他部分以前，能够对程序的状态作统一的管理。无论try所指定的程序块中是否抛出异常，finally所指定的代码都要被执行。通常在finally语句中可以进行资源的清除工作。如：关闭打开的文件，删除临时文件

```
public class Test01 {
    public static void main(String[] args) {
        Testyichang  testyichang = new Testyichang();
        try {
            testyichang.method1();
        } catch (Exception e) {
            System.out.println("uuuuuuuu");
        }
    }
    public void method1() throws Exception{
        method2();
    }
    public void method2() throws Exception{
        method3();
    }
    public void method3() throws Exception{
    }
}
// 执行结果
uuuuuuuu
```
```
public class Testyichang {
    public static void main(String[] args) {
        Testyichang  testyichang = new Testyichang();
        try {
            testyichang.method1();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    public void method1() throws Exception{
        method2();
    }
    public void method2() throws Exception{ 
        method3();
    }
    public void method3() throws Exception{
        throw new Exception("hhhh");
    }
}
// 指定结果
java.lang.Exception: hhhh
	at com.sangyu.Testyichang.method3(Testyichang.java:19)
	at com.sangyu.Testyichang.method2(Testyichang.java:16)
	at com.sangyu.Testyichang.method1(Testyichang.java:13)
	at com.sangyu.Testyichang.main(Testyichang.java:7)
```

![](https://upload-images.jianshu.io/upload_images/2765653-0ed7ddde3330777d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

使用自定义异常一般有如下步骤：
1）通过继承```java.lang.Exception ``` 类声明自己的异常类
2）在方法适当的位置生成自定义异常的实例，并用throw语句抛出
3）在方法的声明部分用throws语句声明该方法可能抛出的异常

```
public class Test03 {
    public void regist(int num) throws Exception {
        if (num < 0) {
            throw new MyException("人数为负值，不合理", 3); // throw 后面的语句不会再执行了
        }
        System.out.println("登记人数" + num);
    }

    public void manager() {
        try {
            regist(-1);
        } catch (MyException e) {
            System.out.println("登记失败，出错类型码 = " + e.getNum());
            e.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        }
        System.out.println("操作结束");
    }

    public static void main(String[] args) {
        Test03 test03 = new Test03();
        test03.manager();
    }
}

class MyException extends Exception {

    int num;
    public MyException(String message, int num) {
        super(message);
        this.num = num;
    }

    public int getNum(){
        return num;
    }
}
// 执行结果：
登记失败，出错类型码 = 3
操作结束
com.sangyu.MyException: 人数为负值，不合理
	at com.sangyu.Test03.regist(Test03.java:6)
	at com.sangyu.Test03.manager(Test03.java:13)
	at com.sangyu.Test03.main(Test03.java:25)
```


## Java- Class.forName() 和 Xxx.class

每个类都有一个Class对象。就是说，每当编写并且编译了一个新类，就会产生一个Class对象，被保存在一个同名的.class文件中。c

所有的类都是在第一次使用时，动态加载到JVM中的。比如使用new操作符创建类的新对象（构造器是默认类的静态方法）。

一旦某个类的Class对象被载入内存，它就被用来创建这个类的所有对象。

```
class Candy{
    static {
        System.out.println("Loading Candy");
    }
}

class Gum{
    static {
        System.out.println("Loading Gum");
    }
}

class Cookie{
    static {
        System.out.println("Loading Cookie");
    }
}

public class SweetShop {
    public static void main(String[] args) {
        System.out.println("inside main");
        new Candy();
        System.out.println("After creating Candy");
        try {
            Class.forName("com.sangyu.test.test21.Gum");
        } catch (ClassNotFoundException e) {
            System.out.println("Could not find Gum");
        }

        System.out.println("After Class.forName(\"Gum\")");
        new Cookie();
        System.out.println("After creating Cookie");
    }
}
```

上面例子中，每个类Candy、Gum、Cookie，都有一个static子句，该子句在类第一次被加载时执行。这时会有相应的信息打印出来，告诉我们这个类什么时候被加载了。

```Class.forName("Gum")``` 这个方法是Class类的静态方法，需要用一个包含目标类的文本名（注意拼写和大小写）的String作为输入参数，返回的是Class对象的引用。这个方法还有一个其他的作用：如果类Gum没有被加载的情况，调用这个方法时就会被加载。在加载过程中，Gum的static子句被执行

```
package com.sangyu.test.test21;

interface HasBatteries{}
interface Waterproof{}
interface Shoots{}

class Toy{
    Toy(){}
    Toy(int i){}
}

class FancyToy extends Toy implements HasBatteries,Waterproof,Shoots{
    FancyToy(){
        super(1);
    }
}
public class ToyTest {
    static void printInfo(Class cc){
        System.out.println("Class name: " + cc.getName() + " is interface? [" + cc.isInterface() + "]");
        System.out.println("Simple name: " + cc.getSimpleName());
        System.out.println("Canonical name: " + cc.getCanonicalName());
        System.out.println("------------------------------------------------");
    }

    public static void main(String[] args) {
        Class c = null;
        try{
            c = Class.forName("com.sangyu.test.test21.FancyToy"); //
        } catch (ClassNotFoundException e) {
            System.out.println("Can't find FancyToy");
        }
        printInfo(c);
        for(Class face : c.getInterfaces()){
            printInfo(face);
        }
        Class up = c.getSuperclass();
        Object obj = null;
        try {
            obj = up.newInstance();
        } catch (IllegalAccessException e) {
            System.out.println("Can't instantiate");
        } catch (InstantiationException e) {
            System.out.println("Can't access");
        }
        printInfo(obj.getClass());
    }
}
```

FancyToy 继承Toy并实现HasBatteries,Waterproof,Shoots接口，main()方法中创建了Class的引用，并将其指向了FancyToy。printInfo()方法中getName()获得全限定的类名，isInterface()判断是否为接口，getSimpleName()获得不含包名的类名，getCanonicalName()获得全限定的类名。main()方法中其他的方法比如getInterfaces()返回Class中所包含的接口，getSuperclass()获得基类，newInstance() 创建实例。在上面例子中，getSuperclass()获得的class引用指向了up，在创建实例时，Object的引用指向的是Toy对象。另外，使用newInstance() 来创建的类，必须带有默认的构造器

Java还提供了另一种方法来生成对Class对象的引用，对上述程序可以这么写：FancyToy.class; 这样做不仅要简单，而且更安全，因为它在编译时就会受到检查（因此不需要置于try语句块中），并且根除了对forName()方法的调用，所以也更高效。

当使用.class来创建对Class对象的引用时，不会自动地初始化该Class对象。

```
class Initable{
    static final int staticFinal = 47;
    static final int staticFinal2 = ClassInitialization.rand.nextInt(1000);
    static {
        System.out.println("Initializing Initable");
    }
}

class Initable2{
    static int staticNonFinal = 147;
    static {
        System.out.println("Initializing Initable2");
    }
}

class Initable3{
    static int staticNonFinal = 74;
    static {
        System.out.println("Initializing Initable3");
    }
}
public class ClassInitialization {
    public static Random rand = new Random(47);

    public static void main(String[] args) throws ClassNotFoundException {
        Class initable = Initable.class;
        System.out.println("After creating Initable ref");

        System.out.println(Initable.staticFinal);
        System.out.println(Initable.staticFinal2);
        System.out.println(Initable2.staticNonFinal);

        Class initable3 = Class.forName("com.sangyu.test.test21.Initable3");
        System.out.println("After creating Initable3 ref");
        System.out.println(Initable3.staticNonFinal);
    }
}
```

在上述例子中，Initable引用的创建不会引发初始化，Class.forName("Initable3") 立即进行了初始化。static final 修饰的值是编译器常量，Initable类没有初始化就可以访问，但staticFinal2并非编译器常量，所以在访问时强制进行类的初始化。Initable2.staticNonFinal 是一个static域不会final的，在对它访问时，要先进行链接（为这个域分配存储空间）和初始化（初始化该存储空间）。

## Java - 反射机制（reflction）

Class类与java.lang.reflect类库一起对反射的概念进行了支持，该类库包含了Field、Method以及Constructor类。这些类型的对象是由JVM在运行时创建的，用以表示未知类里对应的成员。所以可以使Constructor创建新的对象，用get()和set()方法读取和修改与Field对象关联的字段，用invoke()方法调用Method()对象关联的方法。另外还可以调用getFields()、getMethods()和getConstructors()等方法，以返回表示字段、方法以及构造器的对象的数组。这样，匿名对象的类信息就能在运行时被完全确定下来，而在编译时不需要知道任何事情。

Class.forName()生成的结果在编译时不可知的。因此所有的方法特征签名信息都是在执行时被提取出来的。反射机制提供了足够的支持，使得能够创建一个在编译时完全未知的对象，并调用此对象的方法。

```
package com.sangyu.test.test21;

public class User {

    private int id;
    private String name;
    private int age;

    public void setId(int id) {
        this.id = id;
    }

    public int getId() {
        return id;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", age=" + age +
                '}';
    }

    public User(){}
    public User(int id,String name,int age){
        this.id = id;
        this.name = name;
        this.age = age;
    }
}
```

```
package com.sangyu.test.test01;

import java.lang.reflect.Constructor;
import java.lang.reflect.Method;

public class ShowMethods {

    public static void main(String[] args) throws ClassNotFoundException {
        Class<?> c = Class.forName("com.sangyu.test.test21.User");
        Method[] methods = c.getMethods();
        Constructor[] constructors = c.getConstructors();
        for(Method method:methods){
            System.out.println(method);
        }

        System.out.println("");

        for(Constructor constructor:constructors){
            System.out.println(constructor);
        }
    }
}
```
getMethods()和getConstructors()方法分别返回Method对象的数组和Constructor对象的数组。



