写在前面
================

这里是Ozelot。一个正在学习编程，希望和各位大佬一起交流学习的大学生。这是我们设计团队关于编程语言Cesno的**设计方案**，欢迎大家评论交流!

提示: 最终设计尚未决定，可能还有很多设计上的不足需要优化，故内容可能会发生变动。因为没法不加标签，我不得不打了“程序员”标签。希望没有给大家造成困扰。

注意: 因为Cesno并未制作完成，这里只记录Cesno的语法规范。正因如此，代码部分的高亮可能不能保证每一次都正确显示。如果影响了阅读，我感到十分抱歉!

----

关于循环和迭代
================

for循环
================

for循环是编程语言中的常见的循环结构。Cesno包含两种for循环——自定义循环和迭代器循环。创建自定义for循环需要**先写出关键字`for`**，之后书写一个以上，由括号包含的**迭代器定义**。

## 自定义循环

自定义for循环的迭代器定义最为原始。为了创建它，首先需指定一个或以上的**迭代指示器**，再写出**循环体**。**迭代指示器**由**变量声明**、**运行条件**和**迭代后操作**组成。类似于这样`for 迭代指示器1 迭代指示器2`，其中，迭代指示器为`(变量声明; 运行条件; 迭代后操作)`。

如下是最简单的自定义循环的示例:

```c++
for (int i = 0; i < 10; i++)
{
    print(i);
}
```

在`for`循环后，给出了一个迭代指示器`(int i = 0; i < 10; i++)`；且它的变量声明为`int`型的`i`，运行条件是`i`小于`10`；在迭代之后，`i`会被加`1`，直到迭代停止。

### 循环流程控制——当你想更加自由地改变顺序时

当你渐渐接触更多编程实例时，你总会发现，单是一个for循环，似乎不能那么好地完成我的需求。因此，大部分编程语言都提供了可以控制循环的流程的关键字，`continue`和`break`，自然，我们也提供这个。

### 多指示器并行

同样，也可以使用**多个迭代指示器**。需要注意的是，多重迭代器的运行条件相当于: 把所有的**迭代指示器**的**运行条件**以`and`连接。以下是一个例子:

```python
// #从第 2 行到第 10 行是第一段，和第二段是等价的
int a = 0;
float b = 0;
for (;;)
{
    print(a, b);
    if (not (a < 10 and b < 5)) { break; }
    a += 1;
    b += 1;
}

// #从第 13 行到第 16 行是第二段，和第一段是等价的 
for (int a = 0; a < 10; a++) (float b = 0; b < 5; b++)
{
    print(a, b);
}

// #也可以这样声明两个计数器用于 for 循环
for (int a, b = 0, 0; a < 3 and b < 5; a++; b++;)
{
    print(a, b);
}

for ({ int a = 0; string b = "0"; }; a < 3 and b.compareTo("5"); { a++; b++; })
{
    
}

b &= 1;
b := b & 1;
b ^= 1;
b := b xor 1;
b |= 1;
b := b or 1;

for (int base = a; b > 0; { base *= base; base %= p; b = b >> 1; })
```

## 迭代器循环

使用迭代器循环可以简化迭代的书写过程。迭代器循环的结构是: `for x in y`。其中，`x`部分是**变量声明**；`in`是表示采用迭代器循环的关键字；`y`部分可以是一个**可迭代的元素**(即它的类是`Iterable`的)，也可以是一个**迭代器**。

### 可迭代元素

Cesno预先定义了一些可迭代元素，比如`array`、`list`、`tuple`等。案例如下:

```typescript
for (var a in [1, 2, 3])
{
    print(a);
}
```

本例中，`[1, 2, 3]`被推导成`int[]`(即`array<int>`)，而`int[]`是可迭代的。当把可迭代元素直接放在`in`后时，Cesno会使用该元素的提供的迭代器。对于大多数的可迭代元素，其迭代器都是**迭代其可被访问到的元素**。

### 迭代器

Cesno拥有迭代器类`iterator`。它可以

### 设置停止条件

当不指定循环停止条件时，当**迭代器循环**都没有下一个元素时，循环会停止。

看上去似乎迭代器循环并没有办法手动控制它什么时候停止，其实并非如此。只要在**变量声明**后加上**运行条件**即可，就像**自定义循环**一样。

```typescript
for (var x in [1, 6.5, 300, 20]; x < 150)
{
    print(x);    // 打印 1，换行，打印 6.5
}
```


### 多指示器并行

当需要同时使用多个**迭代器循环**时，可以像这样书写:

```typescript
for (var a in [1, "2"]) (var b in [6, "8"])
{
    print(a, b);    // 第一次打印 1 6，第二次打印 2 8。
}
```

并行时，可以通过`continue var_name`的方式，使某个特定的变量获取该迭代器的下一个元素，并继续这个循环。

```typescript
for (var a in [1, "2"]) (var b in [6, "8"])
{
    if (a != undefined) { print(a, b); continue a; }   // 打印出 1 6，换行，再打印出 2 6。
}
```

当一个迭代器不能给出下一个元素时，它会返回`undefined`。

```typescript
for (var a in [1, "2", 4]) (var b in ["6", 10])
{
    print(a, b);
    while (a != undefined or b != undefined) { continue; }
    // 打印 1 6，换行
    // 打印 2 10，换行
    // 打印 4 undefined
}
```



# while循环

# 高级技巧

## then子句和else子句

循环结束存在着两种状况(无异常发生时)，一是**所有循环指示器正常运行完**(正常终了)，二是**循环被break指令强制终止**(流程停止)。此时，可以在for循环后附加then或else子句，来为这些特殊情况做处理。当循环**正常终了**时，then子句会被执行；如果循环**流程停止**，else子句会被执行。

```c++
try for (int i = 0; i < 10; i++)
{
    if (int(input()) == 0) { break; }
}
then
{
    print("No number is 0.");
}
else
{
    print("This number is 0.");
}
catch (NumberFormatError e)
{
    e.printDetail();
}
```

```c++
int a = try { loop { int(input("a: ")); } } catch (Error e) { print("Input again"); };
int b = try 
            loop int(input("b: "));
        catch (Error e)
            print("Input again");
```





## 容器推导式

类似于python，Cesno也有可以快速生成容器的**容器推导式**。

容器推导式字面量的语法是

```
literal (#operand)
{
    ($bracket body) => (
        $expression summon,
        $keyword.cesno.for for_keywd,
        $iteration.indicator... indicators: $len > 0 {
            $if ($len == 1) { $self.can_without_surrounding = $true; }
        }
     )
}
```





```python
int[] a = [i * 2 for (int i in range(4))];    //# 将生成 [0, 2, 4, 6]
```



