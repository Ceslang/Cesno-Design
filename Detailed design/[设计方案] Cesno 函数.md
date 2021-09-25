写在前面
================

这里是Ozelot。一个正在学习编程，希望和各位大佬一起交流学习的大学生。这是我们设计团队关于编程语言Cesno的**设计方案**，欢迎大家评论交流!

提示: 最终设计尚未决定，可能还有很多设计上的不足需要优化，故内容可能会发生变动。因为没法不加标签，我不得不打了“程序员”标签。希望没有给大家造成困扰。

注意: 因为Cesno并未制作完成，这里只记录Cesno的语法规范。正因如此，代码部分的高亮可能不能保证每一次都正确显示。如果影响了阅读，我感到十分抱歉!

----

函数的基础
================

## 函数是什么



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

## 参数状态限制

**参数状态限制**可用于快速判断函数接收的参数**是否可用于该函数**。要创建它，只需要在参数名后加上冒号，并加上希望的**状态限制子**即可。

状态限制子有以下几种形式: 类，形容，或是可以被评价为`bool`的语句。使用`a|b`来代表可以是`a`或`b`状态，使用`a&b`来代表不仅要是`a`且要是`b`状态。

### 类限制子

当需要用多态处理函数，但只希望接收部分子类的实例做参数时，可以采用类限制子。

```typescript
function void printCryOf(Animal a: Cat|SmallDog)
{
    print(a.cry());
}
```

这个例子

### 形容限制子

### `boolean`限制子

比如这个计算平方根的函数:

```typescript
function double my_sqrt(double x: x>=0)
{
    // Some statement
    return sqrt_x;
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

# 匿名函数



# 函数做参数

因为函数也是一种

