写在前面
================

这里是Ozelot。一个正在学习编程，希望和各位大佬一起交流学习的大学生。这是我们设计团队关于编程语言Cesno的**设计方案**，欢迎大家评论交流!

提示: 最终设计尚未决定，可能还有很多设计上的不足需要优化，故内容可能会发生变动。因为没法不加标签，我不得不打了“程序员”标签。希望没有给大家造成困扰。

注意: 因为Cesno并未制作完成，这里只记录Cesno的语法规范。正因如此，代码部分的高亮可能不能保证每一次都正确显示。如果影响了阅读，我感到十分抱歉!

----

# 前置知识

这里将要写有关于**语言部件**的前置基础知识。

## 宏 (Macro)是什么

> ##### [维基百科](https://zh.wikipedia.org/wiki/%E5%B7%A8%E9%9B%86)中对于**宏**的定义
>
> 计算机科学里的宏是一种抽象（Abstraction），它根据一系列预定义的规则替换一定的文本模式。解释器或编译器在遇到宏时会自动进行这一模式替换。对于编译语言，宏展开在编译时发生，进行宏展开的工具常被称为宏展开器。

## C++等语言中的宏

### 运行宏

C++ 的宏分为 define 和 typedef，前者允许用户定义一个标识符为一个字符串（里面允许有参数）；后者允许用户将一个字符串定义为一个数据类型。例如：

```c++
#define mian main                                  // 将全文的 mian 替换为 main

#define rep(i, a, b) for(int i = a; i <= b; ++ i)  // 将全文的 rep(i, a, b) 替换为
                                                   // for(int i = a; i <= b; ++ i)

                                                   // 此时里面的 a, b 都是数值。
                                                   // 例如，调用 rep(i, 1, n) 那么就会
                                                   // 替换为 for(int i = 1; i <= n; ++ i)

typedef myPair pair<int, pair<int, char>>          // 将 pair<int, pair<int, char>> 类型替换为
                                                   // myPair 类型（仅仅替换数据类型）
                                                   // 也就是说，代码其余的 myPair 不会被替换
```

### 编译宏

在 Cesno 编译的过程中，你可以选择在编译选项加上 `--YOUR-OPTION`，使得源代码的以下内容被执行：

```c++
#ifdef YOUR-OPTION { /* Your Code here... */ }
```

例如，源代码如下。

```c++
int a = 10, b = 20;

ifdef cesno {
    a = 20;
}

void main() {
    print(a + b);
}
```

当加入了 `--cesno` 的编译选项的时候，输出是 40，否则输出为 30。

## 从**宏**到**语言部件**

在Cesno中，每当你写下诸如`TYPE_NAME IDENTIFIER;`时，你就定义了一个类型为`TYPE_NAME`的，名为`IDENTIFIER`的变量。==我为什么在这里写了这句== ==我好像又知道了==

在C++里的`typedef`，在Cesno里可以像定义变量一样书写:

<div
    style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em; font-size: 14.5px;">
    <span style="color: #9ed44c; font-weight: bold;">type MyPair</span> <span
        style="color: #a59aca; font-weight: bold;">=</span>
    <span style="color: #9ed44c; font-weight: bold;">pair</span>&lt;<span
        style="color: #9ed44c; font-weight: bold;">int</span>, <span
        style="color: #9ed44c; font-weight: bold;">pair</span>&lt;<span
        style="color: #9ed44c; font-weight: bold;">int</span>,<span
        style="color: #9ed44c; font-weight: bold;">char</span>&gt;&gt; ;
</div>





语言部件的使用
================

## 一些基础概念

本质上来说，Cesno所有代码**都是**宏。机器并不能直接识读Cesno代码，它只能通过读取CPU指令来完成固定的工作。编程语言可以被转换成机器语言供机器识读。

语言部件可以嵌套。

### 语句是什么

一般来说，一个**语句**(statement)是从代码的<u>逻辑行</u>开始，直到<u>逻辑行结尾的分号</u>的部分。下面是一些语句的示范:

<div style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em">
    <span style="color: #9ed44c"><b>string</b></span> <span style="color: #f39800">s</span>
    <span style="color: #A59ACA; font-weight: bolder;">=</span>
    <span style="color: #2ca9e1">input</span>() ; <br>
    <span style="color: #9ed44c"><b>float</b></span> <span style="color: #f39800">f</span> ; <br>
    <span style="color: #E95295">10</span> ; <br>
    <span style="color: #2ca9e1">print</span>("<span style="color: #98623C">Some content to display</span>") ; <br>
</div>


语句包括了以下几种类型:

* 函数或方法单独成句
* 变量声明或赋值，或是标识符的定义
* 语言部件的管理 (例如，说明之后出现的语句是需要单步等待的`await`语句)

### 评价值

**评价值**(evaluated value,简称为evalvalue)是一个语言部件必定拥有的一种“属性”。评价值可以是一个函数的返回值，一个操作符的运算结果或是其它被定义出的评价结果。



在Cesno的每一个非空语句中，必定有一个语言部件，来给出这个语句的作用。

## 为你的语言部件下定义

就像其它的编程语言一样，Cesno也有关键字、类型名、操作符等等概念。这些概念帮助Cesno的编译器更好的编译代码，也帮助我们更好地书写代码。



## 让这个部件工作起来

### eval关键字

eval可以使一个语言部件立即被评价成一个值，类似于Rust中<u>不加分号的语句</u>。当在语言部件的**定义**或是**使用**中，写下诸如`eval VALUE`的句子时，该语言部件会被视作`VALUE`，交给更外层的代码。因为eval会使得该部件被立即评价(就像对于函数而言的`return`)，所以在同一个层级，并在eval语句后的语句，无法被执行到。

在下面的例子中，逻辑判断块(包含`if`和`else`)可以在结束后，被评价成一个值。注意，在eval之后的同级语句，并不会被执行。

```python
int x = int(input("Input one int: "));
int y = if (x > 0)
        {
            print("x is bigger than 0");
            eval 1;
            print("I am unreachable");
        }
        else { eval 0; };
```

## 示例

1. 定义一个会持续循环的`loop`结构——使用loop作为关键字，接受一个代码块，并循环地调用代码块，直到得到停止信号。实现方法为，将代码块放入`while(true)`后执行。

<div
        style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em">
        <span style="color: #c4a3bf; font-weight: bold;">macro</span> <span
            style="color: #9ed44c; font-weight: bold;">$keyword.flow</span> <span
            style="color: #bc64a4; font-weight: bold;">loop</span> 
        <br>
        { <br>
        &nbsp;&nbsp;&nbsp;&nbsp;(<span style="color: #9ed44c; font-weight: bold;">$codeseg</span> <span
                                       style="color: #f39800;">$c</span>)
        <span style="color: #c4a3bf; font-weight: bold;">=></span> <br>
        &nbsp;&nbsp;&nbsp;&nbsp;{ <br>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span
            style="color: #bc64a4; font-weight: bold;">while</span>(<span
            style="color: #c5c56a; font-weight: bold;">true</span>) <span style="color: #f39800;">$c</span> ; <br>
        &nbsp;&nbsp;&nbsp;&nbsp;} <br>
        }
</div>
诸如`$keyword.flow`、`$codeseg`这类名称，是被Cesno保留的、用于宏或者代码解析的特殊的类型。这些类型被以更底层的方式定义，所以一般无法像查看`int`的类型定义那样看它们的定义。

定义好`loop`后，你便可以在引入了它的地方使用它，像这样:

<div style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em">
    <span style="color: #bc64a4; font-weight: bold;">loop</span>
    <br>
    {<br>
    &nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #2ca9e1">print</span>("<span style="color: #98623C">This loop will never end! Use Ctrl + C to
        force stop.</span>") ; <br>
    }
</div>

2. 定义三目运算符`?:`。

<div style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em">
    <span style="color: #c4a3bf; font-weight: bold;">macro</span> <span
        style="color: #9ed44c; font-weight: bold;">$operator.ternary</span> <span
        style="color: #a59aca; font-weight: bold;">? :</span>
    <br>
    { <br>
    &nbsp;&nbsp;&nbsp;&nbsp;(<span style="color: #9ed44c; font-weight: bold;">$condition</span> <span
        style="color: #f39800;">$c</span>),
    (<span style="color: #9ed44c; font-weight: bold;">$codeseg</span> <span style="color: #f39800;">$br1</span>),
    (<span style="color: #9ed44c; font-weight: bold;">$codeseg</span> <span style="color: #f39800;">$br2</span>)
    <span style="color: #c4a3bf; font-weight: bold;">=></span> <br>
    &nbsp;&nbsp;&nbsp;&nbsp;{ <br>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #bc64a4; font-weight: bold;">if</span> (<span
        style="color: #f39800;">$c</span>) <span style="color: #f39800;">$br1</span> <span
        style="color: #bc64a4; font-weight: bold;">else</span> <span style="color: #f39800;">$br2</span>
    ; <br>
    &nbsp;&nbsp;&nbsp;&nbsp;} <br>
    }
</div>
3. 定义`import with`结构，用后置的方法，从一个模块中引入一些函数。

<div style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em">
    <span style="color: #c4a3bf; font-weight: bold;">macro</span> <span
        style="color: #9ed44c; font-weight: bold;">$keyword.namespace</span> <span
        style="color: #c4a3bf; font-weight: bold;">import with</span>
    <br>
    { <br>
    &nbsp;&nbsp;&nbsp;&nbsp;(<span style="color: #9ed44c; font-weight: bold;">$module.path</span> <span
        style="color: #f39800;">$p</span>),
    (<span style="color: #9ed44c; font-weight: bold;">$identifier...</span> <span style="color: #f39800;">$idens</span>)
    <span style="color: #c4a3bf; font-weight: bold;">=></span> <br>
    &nbsp;&nbsp;&nbsp;&nbsp;{ <br>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #c4a3bf; font-weight: bold;">import</span> <span
        style="color: #f39800;">$idens</span> <span style="color: #c4a3bf; font-weight: bold;">from</span> <span
        style="color: #f39800;">$p</span> ; <br>
    &nbsp;&nbsp;&nbsp;&nbsp;} <br>
    }
</div>