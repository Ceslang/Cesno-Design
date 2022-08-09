写在前面
================

这里是Ozelot。一个正在学习编程，希望和各位大佬一起交流学习的大学生。这是我们设计团队关于编程语言Cesno的**设计方案**，欢迎大家评论交流!

提示: 最终设计尚未决定，可能还有很多设计上的不足需要优化，故内容可能会发生变动。因为没法不加标签，我不得不打了“程序员”标签。希望没有给大家造成困扰。

注意: 因为Cesno并未制作完成，这里只记录Cesno的语法规范。正因如此，代码部分的高亮可能不能保证每一次都正确显示。如果影响了阅读，我感到十分抱歉!

----

# 名义类型

## 类

> **类**是什么? 类是**蓝图**。



## 成员



无论是何种类型，类型的成员都可以通过编写属于其的`get`/`set`函数，来防止直接用等号修改其值。

## 动作

动作包含了**函数**和**方法**。

## 属性



## 创建类的实例



## 运算符重载



### 基础

运算符重载形如`return_type operatorx(param_type param ...)`。下面的示例是一个加号的重载。

```c++
class Test
{
    public int x;
    
    operator Test +(int y) { this.x += y; return this; }
}

void main()
{
    Test t;
    t.x = 10;
    print(x + 10);
    print(x.operator+(10));
}
```

事实上，任何运算符都可以被理解成一个方法。比如上例中的`x.operator+(10)`和`x + 10`是等价的。

### 四则运算

四则运算`+`、`-`、`*`、`/`的重载较相似。重载分为**主左运算**和**主右运算**。



# 结构类型

## 结构体





# 原型类型

## 原型类型 和 原型对象

**原型类型**也是类型的一种，可以用来初始化一个**原型对象**。

通过`proto`来创建一个原型类型。如果有现有的变量，可以通过这个变量创建。

<div
    style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em; font-size: 14.5px;">
    <span style="color: #9ed44c; font-weight: bold;">proto</span> <span
        style="color: #5f984d; font-weight: bold;">Potion</span> <span
        style="color: #68be8d; font-weight: bold;">derives</span> <span
        style="color: #5f984d; font-weight: bold;">Item</span><br>
    {<br>
    &nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #9ed44c; font-weight: bold;">int</span> <span
        style="color: #d9a62e">effect_to_hp</span> ;<br>
    &nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #9ed44c; font-weight: bold;">int</span> <span
        style="color: #d9a62e">effect_to_mp</span> ; <br>
    <br>
    &nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #0094c8; font-weight: bold;">method</span> <span
        style="color: #2ca9e1;">effectMulBy</span>(<span style="color: #9ed44c; font-weight: bold;">float</span> <span
        style="color: #e0a37e">times</span>) ; <br>
    }
</div>

上面的例子演示了一个继承自“道具”(Item)类的“药水”(Potion)类。

## 继承方式

所有的原型类型都是通过**链式继承**得来的，每一个对象都有自己的原型，那个原型又拥有它自己的原型，这样就形成了**原型继承链**。在创建原型类型对象时，它们都默认地具有一个基础的原型`ProtoObject`。

当某个原型类型对象找不到自身的某个属性(包括字段、函数、方法)时，它就会按照这条继承链寻找，直到找到继承的终点，`nihilo`。`nihilo`是一个没有任何属性的原型对象，且`ProtoObject`继承自`nihilo`。





# 泛型



值得注意的是，泛型的名字最好和变量一样——不要用像`K`、`V`这样的单个大写字母，而是用`KeyType`、`ValueType`等可以说明泛型作用的名称(甚至可以使用`TypeDeKey`，只要能说明清楚，并易于阅读)。

# 类型编程

## 从不是类型的

## 关于类型的运算

类型也可以参与

# 声明类型的存在

并不是所有函数、类型都有源代码可以追溯，有时它们会存在于各种文件中，但你无法快速知道它们都是谁。此时可以用`declare`来声明它们的存在。`declare`会把后方出现的无论是函数、类型、还是变量等，全部作为声明出现。此时如果尝试去赋予具体定义，则会报错。

## `declare`和**直接声明**的区别

假设你直接声明了一个函数`f`:

<div
    style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em; font-size: 14.5px;">
    <span style="color: #0094c8; font-weight: bold;">function</span> <span
        style="color: #9ed44c; font-weight: bold;">int</span> <span style="color: #2ca9e1;">f</span>();
</div>

你尝试调用它，结果编译前就会得到一个错误: `f`的值为`undefined`。

但假设你尝试宣言`f`的存在:

<div
    style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em; font-size: 14.5px;">
    <span style="color: #68be80; font-weight: bold;">declare</span> <span
        style="color: #0094c8; font-weight: bold;">function</span> <span
        style="color: #9ed44c; font-weight: bold;">int</span> <span style="color: #2ca9e1;">f</span>();
</div>

编译前，你使用它就不会有任何错误报告。但是，`f`的具体定义必须是存在的。如果编译器在编译时找不到`f`的定义，照样会报错。

## 声明函数

