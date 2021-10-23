写在前面
================

这里是Ozelot。一个正在学习编程，希望和各位大佬一起交流学习的大学生。这是我们设计团队关于编程语言Cesno的**设计方案**，欢迎大家评论交流!

提示: 最终设计尚未决定，可能还有很多设计上的不足需要优化，故内容可能会发生变动。因为没法不加标签，我不得不打了“程序员”标签。希望没有给大家造成困扰。

注意: 因为Cesno并未制作完成，这里只记录Cesno的语法规范。正因如此，代码部分的高亮可能不能保证每一次都正确显示。如果影响了阅读，我感到十分抱歉!

----

函数的基础
================

## 函数是什么

和大多数编程语言相同，**函数**是既定的，一系列命令、动作的集合体。它既可以处理一些数据，让这些数据变成你希望的样子；又可以包装一串命令，让你可以更短地书写它们……

## 函数的定义

函数定义以`function`关键字开始，加上**返回值类型**、**函数名**以及**参数列表**构成。如下:

```typescript
function return_type func_name(param_type param_1, param_type param_2)
{
    // Some statement
    return return_type(x);
}
```

```typescript
function int plusOne(int x)
{
    return x + 1;
}
```

函数也是一种数据类型。因此，可以像这样声明一个函数。

```typescript
function<(number, number), number> add = (x, y) => { return x + y; };
```

等号右半部分可能现在看起来有些令人费解。它是一个**匿名函数**，将在本页面之后的部分被讨论。现在只需记住这个**匿名函数**也是一个**函数**即可。

# 参数

## 参数是什么

**参数**可以看作一个函数的**接入点**。参数**接收**了对应位置的数据，并**传递**给函数来处理。



# 匿名函数



# 函数做参数

因为函数也是一种




# 参数高级技巧

## 默认参数

使用默认值的参数应该**全部位于**必须传入的参数**之后**。

假设如果不这样书写，那么拥有两个重载`void f(int a, int b=3, int c)`是

## 参数接受限制

### 必须传入该参数

如果希望使用者必须传入参数，只需直接书写参数即可。如希望用户使用`add`函数时必须传入两个参数，则像这样`int add(int a, int b)`书写即可。

### 只允许指名传参

如果希望使用者必须用`f(0, a=3, b=2+3)`这样的**只在指明接受值的参数名**的形式传递某些参数，则定义函数时，在想要 *只允许指名传参* 的参数前，加入一个新参数，并在这个参数的位置上只写一个`/`作为标记，比如`int add(int x, /, int a, int b)`。需要注意的是，只允许指名传参的参数，必须放在参数元组的**最后方**。

如果上面一段话过于混乱，那简单地说就是，**`/`参数**后面的其他参数只能用 *指定名字* 加 *等号* 加 *想要传入的值* 的形式，才能得到用户输入的值。

举个例子，这一项功能会被用在接收**仅用位置无法明确含义**的参数上。比如若有函数`read`定义为`string read(Writable source, bool check)`，第一个参数是读操作的目标，第二个是读取内容时是否检查；则不检查内容，直接读取某个文件(名称为`doc`)的函数长成这样`read(doc, false)`。单看函数调用，几乎没法弄明白为何会有一个`false`在这里。

### 只允许位置传参

类似地，如果希望使用者必须用`f(0, 3, b=2+3)`这样的形式传递某些参数，则定义函数时，在想要 *只允许位置传参* 的参数前

举个例子，这一项功能可被用在**不希望用户自己指定**上。

## 参数状态限制

**参数状态限制**可用于快速判断函数接收的参数**是否可用于该函数**。要创建它，只需要在参数名后加上冒号，并加上希望的**状态限制子**即可。

状态限制子有以下几种形式: 类，形容，或是可以被评价为`bool`的语句。使用`a|b`来代表可以是`a`或`b`状态，使用`a&b`来代表不仅要是`a`且是`b`状态。

### 类限制子

当需要用多态处理函数，但只希望接收部分子类的实例做参数时，可以采用类限制子。

```typescript
function void printCryOf(Animal a: Cat|SmallDog)
{
    print(a.cry());
}
```

这个例子说明了，接受的参数`a`作为`Animal`传入函数，但要么属于`Cat`类，要么属于`SmallDog`类。

### 形容限制子

### `boolean`限制子

比如这个计算平方根的函数:

```typescript
function double my_sqrt(double x: x>=0)
{
    // Some statement
    return sqrt(x);
}
```

如果使用者用`my_sqrt(-2)`调用它，那编译器就会报出错误。而如果在编译时无法确定值，错误将在最终运行时报出，像这样 (开启了Detailed Report的情况下):

```
Error occured at 09.04.2021 11:36:08 (UTC +08:00).

ParamStateError: -2 is not eligible for parameter state "x >= 0"
    at test.my_sqrt() (line 1): < ParamStateCheck >
    at test.main() (line 1): my_sqrt(double(input()))

Detailed Report for ParamStateError:
    The parameter for function double my_sqrt(double) has parameter restriction,
    however the input parameter does not fulfill it.

    function double my_sqrt(double x):
            parameter double x:
                restrction:  x >= 0
                input:       -2 (int)
                
    Possible solution:
        Value is received by input() function. Change the input value may solve this problem.
        try: replace line 1 at test.main() to the following statement:
            my_sqrt(double(input("Input one x (double) that satisfy \"x >= 0\" ")));
```