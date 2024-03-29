
# <center><font color="#ff5599">浙江大学 翁恺 零基础学Java语言</font></center>

## 第1周 计算
### 1.0 计算机与编程语言

* 1.0.1 计算机与编程语言
    
  * 计算机语言
    * 程序是用特殊的编程语言写出来表达如何解决问题的
    * 不是用编程语言来和计算机交谈，而是描述要求它如何做事情的过程或方法
  * 算法
    * 我们要让计算机做计算，就需要像这样找出计算的步骤，然后用编程语言写出来
    * 计算机做的所有的事情都叫做计算
    * 计算的步骤就是算法

* 1.0.2 计算机的思维方式

  * 程序的执行
    * 解释：借助一个程序，那个程序能试图理解你的程序，然后按照你的要求执行
    * 编译：借助一个程序，就行一个翻译，把你的程序翻译成计算机真正能懂的语言——机器语言——写的程序，然后，这个机器语言写的程序就能直接执行了
  * 解释语言VS编译语言
    * 语言本无编译/解释之分
    * 常用的执行方式而已
    * 编译型语言有特殊的计算能力
    * 编译型语言有确定的运算性能

### 1.1 第一个Java程序

* 1.1.1 准备Java编程软件

  * Eclipse
  * JRE

* 1.1.2 第一个Java程序

    ``` java
    System.out.println("Hello World!");
    ```

### 1.2 变量与计算

* 1.2.1 输入

    ``` java
    import java.util.Scanner;
    // main里输入:
    Scanner input = new Scanner(System.input);
    // 输出输入的一行
    System.out.println(input.nextline());
    ```

    * 字符串连接&nbsp; `+`
    * 注释快捷键&nbsp; `Ctrl + /`

* 1.2.2 变量

  * 变量定义
    * 变量定义的一般形式就是：
      * <类型名称> <变量名称>;
    * int price;
    * int amount;
    * int price , amount;
  * 变量的名字
    * 标识符：它是用来识别这个和那个不同的名字
    * 基本原则：标识符只能由字母、数字和下划线组成，数字不可以出现在第一个位置上，关键字不可以做标识符
  * 变量类型
    * Java是一种强类型语言

* 1.2.3 赋值

  * 赋值
    * 关键字&nbsp; `=`
  * 常量
    * 关键字&nbsp; `final`

* 1.3.1 浮点数

  * 