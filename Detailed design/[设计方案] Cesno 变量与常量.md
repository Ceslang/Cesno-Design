写在前面
================

这里是Ozelot。一个正在学习编程，希望和各位大佬一起交流学习的大学生。这是我们设计团队关于编程语言Cesno的**设计方案**，欢迎大家评论交流!

提示: 最终设计尚未决定，可能还有很多设计上的不足需要优化，故内容可能会发生变动。因为没法不加标签，我不得不打了“程序员”标签。希望没有给大家造成困扰。

注意: 因为Cesno并未制作完成，这里只记录Cesno的语法规范。正因如此，代码部分的高亮可能不能保证每一次都正确显示。如果影响了阅读，我感到十分抱歉!

----

变量的基础
================

这里将要写有关于变量的前置基础知识。如果您已经了解过**标识符**、**类型**等概念，也不妨快速阅读一下。

标识符
----------------

**标识符**是编程语言中不可或缺的一个概念，它代表了一个“东西”的名字(这个东西可以是变量、函数、类……)。

Cesno的标识符和其他语言类似。标识符中可以有数字、英语字母、“$”符号以及“\_”符号，但数字不能出现在标识符的第一个字符。标识符没有长度限制，也允许存在除了一些特殊字符和数字外的其他字符(因为Cesno支持UTF-8编码格式)。但为了可读性、简易性等等原因，标识符不推荐过长(比如超过了64个字符，或任何让人看了摸不着头脑的长度)的名字，也不推荐使用ASCII字符外的其他字符做标识符。

||起始字符|起始字符之后|
|-|-|-|
|数字|×|〇|
|英语字母|〇|〇|
|"$"、"\_"|〇|〇|

同样的，标识符<u>不可以</u>是**关键字**，也<u>不建议</u>和**保留字**或是**修饰符**同名——这样可以避免代码看上去难以理解。

类型
----------------

**类型**是一种用来区分数据的“标准”。数据有了类型，计算机就可以正确存入和读取它们。若没有类型，不仅会给程序员书写程序带来困难，计算机也将更难处理数据。所以，在大部分编程语言中，是不存在真正“没有任何类型”的数据的。

举个例子，在英语中，“main”这个单词是“主要”的意思，而在法语中是“手”的意思。只给你看

如下是在Cesno中常用的几种类型(有些专有名词或缩写，即使目前看不懂也没有关系):

|类型名(英文)|类型名(中文)|简要解释|
|-|-|-|
|`int`|整数型(或“整型”)|存储-2147483648至2147483647的整数，一般拿它存储一个**整数**足够使用|
|`float`|浮点型|遵循IEEE标准中的双精度浮动小数点数，一般用来存储一个**小数**也足够使用|
|`bool`|布尔型(或“真伪型”)|存储一个**真值**(`true`)或一个**伪值**(`false`)|
|`char`|字符型|存储**一个**以UTF-8方式编码的**字符**|
|`string`|字符串型|存储**一系列**以UTF-8方式编码的**字符**|


如想要参阅更多类型或有关于类型的信息，请移至[Cesno 类型一览](./Cesno 类型一览.md)。如果您是初学者，建议先往下看，以后再去了解与类型相关的更多知识。

变量的操作
================

声明与赋值
----------------

**声明变量**需要先写出**类型**的名字，其次写上**变量**的名字(变量名遵循标识符的命名规范)。比如:

```c++
int a;
```

这完成了对一个整数型变量`a`的声明。在接下来的程序中，你就可以使用`a`这个“盒子”，来存放或者读取一个`int`。当然，目前盒子`a`里**什么都没有**，如果你想读取它，就只能发现什么都拿不到。为了之后能读取它，你得先给它添加一些东西:

```c++
a = 10;
```

这里的`=`并不等同于数学上的等号，而更像数学上的`:=`(赋值等号)，它的作用是“让左边的变量接受右边的值”(或者也可以认为是“把右边的值塞到左边那个盒子里去”)。现在，`a`这个盒子里就有了数据`10`。

当然，如果每次你创建这样一个“盒子”时，都希望一开始里面就能够有些东西，你也可以像下面这样写，因为在声明变量时，也可以同时给予其一个初始值:

```c++
int b = 20;
```

Cesno常用类型的声明和赋值如下:

```c++
int    x = 100;
float  d = 0.5;
bool   t = true;
char   c = 'C';
string s = "Hello, everyone.";
object o = 20; // 事实上，object类变量可以接受任何具体类型的赋值
               // 比如上面的类型都可以填入object。
```

## 引用——给予“别名”

当你创建了一个变量时，你就使用了相应大小的空间来存放它；当你把这个变量赋值给另一个新变量时，新的变量就获得了之前变量的<u>值的复制</u>。但可能你并不总是需要复制，有时，你想要使用一个名字来“称呼”一个原有的变量，操作这个名字，等于操作原有的那个变量——这样的技术我们叫做**参照** (refer)。参照一个变量，就获取对它的引用 (reference)；利用引用，我们就可以通过操作新的变量，改变旧变量。

## 盒子里没有东西——两个表示“没有”的值

当一个变量被声明出来，但是并没有赋于初始值 (即“没有被定义”)，Cesno会认为这个变量是`undefined`，未定义的。这个变量盒子里，我们不知道它包含什么，因为这个盒子我们只表明了它的存在，并没有说明盒子里存在什么东西，或者什么都没有。一般来说，对于已经赋值过后的变量，不会再次赋值为`undefined`。

```c++
int a;
print(a)    // 输出 undefined
```

如果想要表达盒子里什么都没有的话，就给这个盒子赋值为`null`。`null`是人为定义的“没有值”，即“我表明这个盒子里什么都没有，是空的”。而`undefined`则表示“我不知道盒子里是什么状态，这个盒子不应该被直接操作”。


销毁
----------------

当你高高兴兴地创造了很多个盒子来保存你的数据时，你可能会忽然发现: 有的盒子只用过一次，就不需要再用了。你想把这个盒子给清空掉，免得有太多用不到的盒子堆在你的代码里。这时，你可以选择销毁他们。这可以用来节约你的内存。使用操作符`delete`可以轻松取消掉变量的声明，并释放内存空间。比如这样:

```c++
int a = 10;
// 一些用到了 a 的代码
delete a;
```

或者把他们“包在一块”——使用一对大括号`{}`来表明一个作用范围。在这个作用范围里声明的任何东西，出了这个范围就被自动摧毁了。

变量工作的范围
================

变量命名空间
----------------

**命名空间**可以用来防止名称冲突。编程人员可以采用`namespace`关键字加上一个标识符来划定一个命名空间。采用“.”(成员访问运算符)可以访问(包括读取和写入)命名空间内的成员，因此作用域内外可以互相访问——从外访问内，使用“.”，从内访问外，只需直接写出名字即可。可以在命名空间内声明和销毁在当前命名空间内的变量，但无法销毁外部变量。

```c++
int a = 10;
namespace n
{
    int b = 20;
    print(a + b);    // 将输出 30，其中 a = 10，b = 20，a 外 b 内
    a = 50;
    print(a + b);    // 将输出 70，其中 a = 50，b = 20，a 外 b 内
    int a = 60;
    print(a + b);    // 将输出 80，其中 a = 60，b = 20，a 内 b 内
}
print(a);      // a 是 10
print(n.a);    // a 是命名空间内成员，为 60
```

也可以创建匿名的命名空间，方式为**不给`namespace`后追加标识符**。比如这段代码:

```c++
int a = 10;
namespace { int anonymous_x = 20; print(anonymous_x); } // 这样写是正确的
// 在这里无法访问 anonymous_x，因为这个命名空间没有名字，你无法写出访问它的式子
```

在类的定义中，如果某一些成员只会给其中一些方法使用，这时我们可以使用`namespcae`来限定，使得这个成员不会被暴露到更多的方法去。关于这一点，可以参照"Cesno 类 型 泛型"(链接的PLACEHOLDER)。

变量作用域
----------------

Cesno像其他语言一样拥有**作用域**(scope)的概念。一个标识符**可以被直接书写出来的范围**就是它的作用域。作用域和命名空间、函数等关系很深。

一个变量在一个命名空间内都有效——也包括了它内部的命名空间:

```c++
int a = 10;
namespace { print(a); /* 正确，可以访问 */ }
print(a); /* 同样正确，可以访问 */
```

定义体内(如函数定义体)无法访问其他定义体的变量，除非它是全局变量:

```typescript
global var n = 10;

class Test
{
    var member = n;    // 可以访问，n 是全局变量
}

function void changeGlobalVarN()
{
    n = "Some string";
}

void main()
{
    var n = 5;               // 在 main 中覆盖了全局 n 的声明，这个 n 是局部的
    Test t1 = new Test();    // 成员 member 是 10
    changeGlovalVarN();
    Test t2 = new Test();    // 成员 member 是 "Some string"
}
```

由上面的例子可知: 全局变量要慎用，否则容易导致错误。

不需要变动的变量
================

## 常量 `const`

**常量**是一个不可变的固定值；一旦赋值，就不允许重新赋值，也不能改变其内部的值。可以通过`const`关键字来定义一个常量，在这个时候，可以省略变量类型信息:

```c++
const int a = 10;    // 之后的 a 的值不可变
int b = a + 10;      // 这样是正确的，b 的值为 20
// a = a + 10;       // 这是错误的，a 不能再次被赋值
```

在这里引入一个额外的概念，作为支持面向对象的语言，Cesno中每一个变量，都可以通过在<u>变量名后加上一个`.` (英文句点)</u>，来访问属于它的一些函数或是**方法** (可以使用或改变这个变量**内部值**的函数)。

假设这里有一个类型叫`ExampleOfConst`的变量`example`，`example`拥有一个名叫`changeInternalValue`的方法，可以改变`example`的某些內部值。我们现在尝试使用这个方法，修改`example`的一些值:

<div style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em">
    <span style="color: #68be8d"><b>const</b></span> <span style="color: #f39800">example</span>
    <span style="color: #A59ACA; font-weight: bolder;">=</span>
    <span style="color: #67a70c"><b>ExampleOfConst</b></span>() ;
    <span style="color: #b3ada0">&nbsp;&nbsp;&nbsp;// To create variable `example` for your example</span><br />
    <span style="color: #f39800;">example</span>.<span
        title="Constants are not able to be modified. This method changes the internal value of the constants."
        style="color: #38a1db; text-decoration: red wavy underline 1.2px; text-decoration-skip-ink: none;">changeInternalValue</span>()
    ;
</div>

## 最终态 `final`

和常量不同的是，将一个量定义为**最终态**并不会导致其内部的值不可被修改。**最终态**表明了一个变量不可再被重新赋值，一个类不可被继承。



需要注意，`const`和指针一起使用时需要注意。关于这一点，请参照“Cesno 指针与引用”(链接的PLACEHOLDER)。



# 有关于变量的更多知识

## 动态类型

如果要声明的变量没有固定的类型(即“动态类型”)，可以采用关键字`var`。这时，Cesno不会在赋值时检查类型是否匹配。动态类型有时可以提供方便，所以请适当地使用它。Cesno的动态类型并不意味着变量“没有类型”。事实上，变量类型一直是静态的，只不过表现为动态。

```typescript
var x = 3;  // 此时，x的类型由字面量 3 推导为 int 型
x += 7;     // x现在等于10，这种写法正确的
x = "str";  // x现在为 string 型，由代入的值 "str" 推导而来
x = 1 / x;  // 这会报错。Cesno在此时能确定 x 在这里就是 string 型，
            // 而除号不适用于 int 与 string 一起运算。
            // 但如果程序流程包含了选择，Cesno便不能确定采用动态类型的变量的具体类型，
            // 而这可能会导致潜在的错误。所以请勿滥用 var 来定义变量。
```

## 自动类型推断 和 自动类型填写

**自动类型推断**指的是: 定义或声明新标识符时，不手动写出其类型，而是由编译器自动将类型推导出来。在之后的代码里，该变量的类型保持推断出的类型不变。

使用`let`可以用**自动类型推断**的方式定义一个变量。

<div style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em">
    <span style="color: #9ed44c"><b>let</b></span> <span style="color: #f39800">string_variable</span>
    <span style="color: #A59ACA; font-weight: bolder;">=</span>
    <span style="color: #2ca9e1">input</span>("<span style="color: #98623C">Input some string: </span>") ;
</div>
这适用于你可以清楚读出<u>变量类型是什么</u>的时候。当你不太清楚等号右边会返回什么类型的时候，可以将`let`改写为`auto let`:

<div style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em">
    <span style="color: #9ed44c"><b>auto let</b></span> <span style="color: #f39800">string_variable</span>
    <span style="color: #A59ACA; font-weight: bolder;">=</span>
    <span style="color: #2ca9e1">some_function_with_implicit_return_type</span>() ;
</div>

当写完这一行，在行末按下回车时，支持该功能的IDE会将`auto let`替换成实际类型，像这样:

<div style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em">
    <span style="color: #9ed44c"><b>string[]</b></span> <span style="color: #f39800">string_variable</span>
    <span style="color: #A59ACA; font-weight: bolder;">=</span>
    <span style="color: #2ca9e1">some_function_with_implicit_return_type</span>() ;
</div>

即使`auto let`可能不会在某些环境生效，但这里`auto`作为`let`的<u>修饰字</u>存在，也不会产生额外的编译错误。

## 与C++的不同点

使用`delete`时，不需要考虑数据类型**是否是数组**，因此，Cesno没有，也不需要有`delete[]`:

```c++
int   a = 20;
int[] b = [30, 50, 100, 200];
delete a, b;
```

当一个使用了多态的变量将要被销毁时，无需强制转换类型:

```c++
object x = 10;
delete x;    // 正确，会释放掉 int 大小的空间，并删除 x 的声明
```

在每一个变量离开作用域时，都会被自动地delete。
