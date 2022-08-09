写在前面
================

这里是Ozelot。一个正在学习编程，希望和各位大佬一起交流学习的大学生。这是我们设计团队关于编程语言Cesno的**设计方案**，欢迎大家评论交流!

提示: 最终设计尚未决定，可能还有很多设计上的不足需要优化，故内容可能会发生变动。因为没法不加标签，我不得不打了“程序员”标签。希望没有给大家造成困扰。

注意: 因为Cesno并未制作完成，这里只记录Cesno的语法规范。正因如此，代码部分的高亮可能不能保证每一次都正确显示。如果影响了阅读，我感到十分抱歉!

----

函数的基础
================

## 函数是什么

和大多数编程语言相同，**函数**是既定的，一系列命令、动作的集合体。它既可以处理一些数据，让这些数据变成你希望的样子；又可以包装一串命令，让你可以更短地书写它们……函数接受一些东西——“参数”，这些参数在函数体内部产生某些作用；函数的处理结果也可以被当作一个评价值——只需从函数中将其**返回**即可。

## 函数的定义

完整的函数定义以`function`关键字开始，加上**返回值类型**、**函数名**以及**参数列表**构成。如下:

```typescript
function return_type func_name(param_type param_1, param_type param_2)
{
    // Some statement
    return return_type_var;
}
```

```typescript
function int plusOne(int x)
{
    return x + 1;
}
```

函数的**返回值类型**不是必须的，参数的类型

函数也是一种数据类型。因此，可以像这样声明一个函数。

<div
    style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em; font-size: 14.5px;">
    <span style="color: #9ed44c; font-weight: bold;">function</span>&lt;(<span
        style="color: #9ed44c; font-weight: bold;">number</span>, <span
        style="color: #9ed44c; font-weight: bold;">number</span>), <span
        style="color: #9ed44c; font-weight: bold;">number</span>&gt;
    <span style="color: #2ca9e1;">sumTwoNumber1</span> <span style="color: #a59aca; font-weight: bold;">=</span>
    <span style="color: #0094c8; font-weight: bold;">function</span>(<span style="color: #e0a37e">left</span>, <span
        style="color: #e0a37e">right</span>) <br>{ <br>
    &nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #bc64a4; font-weight: bold;">return</span>
    <span style="color: #e0a37e">left</span> <span style="color: #a59aca; font-weight: bold;">+</span> <span
        style="color: #e0a37e">right</span> ; <br> }; <br> <br>
    <span style="color: #9ed44c; font-weight: bold;">function</span>&lt;(<span
        style="color: #9ed44c; font-weight: bold;">number</span>, <span
        style="color: #9ed44c; font-weight: bold;">number</span>), <span
        style="color: #9ed44c; font-weight: bold;">number</span>&gt;
    <span style="color: #2ca9e1;">sumTwoNumber2</span> <span style="color: #a59aca; font-weight: bold;">=</span> <br>
    &nbsp;&nbsp;&nbsp;&nbsp;(<span style="color: #e0a37e">left</span>, <span style="color: #e0a37e">right</span>)
    <span style="color: #0094c8; font-weight: bold;">-></span> { <span
        style="color: #bc64a4; font-weight: bold;">return</span>
    <span style="color: #e0a37e">left</span> <span style="color: #a59aca; font-weight: bold;">+</span> <span
        style="color: #e0a37e">right</span> ; } ;
</div>

等号右半部分可能现在看起来有些令人费解。它是一个**匿名函数**，将在本页面之后的部分被讨论。现在只需记住这个**匿名函数**也是一个**函数**即可。

## 关于函数的返回

你可以在函数的任何一个地方让函数停止工作，并把处理过的值作为评价值<u>传递出去</u>。这样的动作叫做“函数的返回”，传递出去的值叫做“返回值”。

函数的返回值在大部分情况下是可以被**自动推断**的，所以，当返回值类型清晰明确时，可以省略返回值类型。

在一个函数可能返回多种类型的值时，函数会被推断为**联合类型**返回——返回值类型可能是其中的任意一种。

`null`和`undefined`也可以作为函数的返回类型。当一个函数可能返回一个`null`时，如果希望用户进行处理，可以写返回值为`SomeClass | null`的形式，这样调用这个函数的人就必须对潜在的`null`返回值作出处理。

函数也可以什么都不返回，此时这个函数便失去了评价值，技术上来说，这相当于`return void`。

## 函数的调用

这和数学上的定义很相似。比如若有$f(x) := x + 2$，则$f(1) + 3 = (1 + 2) + 3 = 6$，就像数学课本上所说的一样。我们在函数后放上一个**包含参数的元组**来让这个函数接受我们给它的参数，开始工作并最终给出一个结果: 这样的行为称为**调用**。

当你定义了一个函数时，如果你只是写出了它的名字，它是不会工作的 (包括这个函数)；直到你给予

# 参数

## 参数是什么

**参数**可以看作一个函数的**接入点**。参数**接收**了对应位置的数据，并**传递**给函数来处理。





# 匿名函数

是否有时也会遇到这样的情况: 有时，一个函数只需要使用一次；有时，需要函数来表达某个动作，但不希望为此就创建一个函数……看起来，似乎我们不是每次都必须创建一个完整的函数来完成我们的工作。并且，就目前的知识来看，新创建函数，也会让我们分配一个名字给它。


# 函数做参数

因为函数也是一种数据，所以也可以作为别的函数的参数传入。

# 函数重载



# 函数模板

有时，为了完成一些工作，你可能需要书写大量的<u>函数重载</u>，而它们可能只完成了极为相似的工作。比如，你为`int`、`float`和`string`书写了`add`函数，而所有的语句都是一样的:

<div
    style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em; font-size: 14.5px;">
    <span style="color: #0094c8; font-weight: bold;">function</span> <span style="color: #2ca9e1;">add</span>(<span
        style="color: #9ed44c; font-weight: bold;">int</span> <span style="color: #e0a37e">a</span>, <span
        style="color: #9ed44c; font-weight: bold;">int</span> <span style="color: #e0a37e">b</span>)
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    { <span style="color: #bc64a4; font-weight: bold;">return</span> <span style="color: #e0a37e">a</span> <span
        style="color: #a59aca; font-weight: bold;">+</span> <span style="color: #e0a37e">b</span> ; } <br>
    <span style="color: #0094c8; font-weight: bold;">function</span> <span style="color: #2ca9e1;">add</span>(<span
        style="color: #9ed44c; font-weight: bold;">float</span> <span style="color: #e0a37e">a</span>, <span
        style="color: #9ed44c; font-weight: bold;">float</span> <span style="color: #e0a37e">b</span>) &nbsp;
    { <span style="color: #bc64a4; font-weight: bold;">return</span> <span style="color: #e0a37e">a</span> <span
        style="color: #a59aca; font-weight: bold;">+</span> <span style="color: #e0a37e">b</span> ; } <br>
    <span style="color: #0094c8; font-weight: bold;">function</span> <span style="color: #2ca9e1;">add</span>(<span
        style="color: #9ed44c; font-weight: bold;">bigint</span> <span style="color: #e0a37e">a</span>, <span
        style="color: #9ed44c; font-weight: bold;">bigint</span> <span style="color: #e0a37e">b</span>)
    { <span style="color: #bc64a4; font-weight: bold;">return</span> <span style="color: #e0a37e">a</span> <span
        style="color: #a59aca; font-weight: bold;">+</span> <span style="color: #e0a37e">b</span> ; }
</div>


此时不妨使用叫做**函数模板**的工具。

<div
    style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em; font-size: 14.5px;">
    <span style="color: #0094c8; font-weight: bold;">function</span> &lt;<span
        style="color: #9ed44c; font-weight: bold;">type</span> <span
        style="color: #00a381; font-weight: bold;">OprandType</span>: <span
        style="color: #a7b446; font-weight: bold;">Addable</span>&gt; <span style="color: #2ca9e1;">add</span>(<span
        style="color: #00a381; font-weight: bold;">OprandType</span> <span style="color: #e0a37e">a</span>, <span
        style="color: #00a381; font-weight: bold;">OprandType</span> <span style="color: #e0a37e">b</span>)
    { <span style="color: #bc64a4; font-weight: bold;">return</span> <span style="color: #e0a37e">a</span> <span
        style="color: #a59aca; font-weight: bold;">+</span> <span style="color: #e0a37e">b</span> ; }
</div>
函数模板可以在保留参数原本类型的情况下，生成一个用于调用类型的独特函数。

如果希望在使用模板时，对某一种类型的参数进行个别处理，可以通过将*一部分或全部的*参数进行指定，来对函数进行**特化**。但请注意，为了不造成困扰，最好提供一个没有任何参数被特化的通用版本。



# 函数高级技巧

## 省略返回值类型

在定义函数时，可以省略返回值的类型，并由Cesno去推断。如果声明函数时省略返回值类型，则该函数推断为返回`any`。

### 当函数不返回值时

当一个函数没有`return`语句时，Cesno会推断返回值是`void`。例如这个函数:

<div
    style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em; font-size: 14.5px;">
    <span style="color: #0094c8; font-weight: bold;">function</span> <span
        style="color: #2ca9e1;">printSomething</span>() <br>
    {<br>
    &nbsp;&nbsp;&nbsp;&nbsp; <span style="color: #2ca9e1;">print</span>("<span style="color: #98623C">Some content to
        display</span>") ; <br>
    }
</div>
如果在所有的情况下都不可能返回，Cesno会推断返回值为`never`。比如:

<div
    style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em; font-size: 14.5px;">
    <span style="color: #0094c8; font-weight: bold;">function</span> <span
        style="color: #2ca9e1;">throwErrorFrom</span>(<span
        style="color: #9ed44c; font-weight: bold;">string</span><span
        style="color: #a59aca; font-weight: bold;">|</span><span
        style="color: #9ed44c; font-weight: bold;">number</span> <span style="color: #e0a37e">reason</span>) <br>
    {<br>
    &nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #bc64a4; font-weight: bold;">match</span> (<span
        style="color: #e0a37e">reason</span>)<br>
    &nbsp;&nbsp;&nbsp;&nbsp;{ <br>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #9ed44c; font-weight: bold;">string</span> <span
        style="color: #c4a3bf; font-weight: bold;">=></span> <span
        style="color: #bc64a4; font-weight: bold;">throw</span> <span
        style="color: #9ed44c; font-weight: bold;">IllegalTextError</span>(<span style="color: #e0a37e">reason</span>)
    ;<br>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #9ed44c; font-weight: bold;">number</span> <span
        style="color: #c4a3bf; font-weight: bold;">=></span> <span
        style="color: #bc64a4; font-weight: bold;">throw</span> <span
        style="color: #9ed44c; font-weight: bold;">NumberOutOfRangeError</span>(<span
        style="color: #e0a37e">reason</span>) ;
    <br>
    &nbsp;&nbsp;&nbsp;&nbsp;}<br>
    }
</div>

在任何一个match分支中，都会抛出一个异常——所以这个函数无论在什么时候，都不会有返回值。

### 当函数有返回值时

当有明确返回值类型时，Cesno会自动推断类型。当函数包含流程控制语句时，Cesno会认为所有<u>非异常结束</u>的流程都具有返回值，并取**联合类型**作为返回。

## 省略参数类型

当使用动态类型风格编程时，可以省略参数的类型`any`，像这样书写`function f(a) { a.someMethod() ; }`。

注意，此时给省略类型的参数名前加任何修饰符，都会作为对该参数可接受的实际参数的类型的限制。比如`(const a)`等同于`(any const a)`。

## 参数默认值

使用默认值的参数应该**全部位于**必须传入的参数**之后**。

假设如果不这样书写，那么拥有两个重载`void f(int a, int b=3, int c)`是

## 参数接受限制

### 必须传入该参数

如果希望使用者必须传入参数，只需直接书写参数即可。如希望用户使用`add`函数时必须传入两个参数，则像这样`int add(int a, int b)`书写即可。

### 只允许指名传参

如果希望使用者必须用`f(0, a=3, b=2+3)`这样的**只在指明接受值的参数名**的形式传递某些参数，则定义函数时，在想要 *只允许指名传参* 的参数们的**前面**，加入一个新参数，并在这个参数的位置上只写一个`*`作为标记，比如`int add(int x, *, int a, int b)`。需要注意的是，只允许指名传参的参数，必须放在参数元组的**最后方**。

如果上面一段话过于混乱，那简单地说就是，**`*`参数**后面的其他参数只能用 *指定名字* 加 *等号* 加 *想要传入的值* 的形式，才能得到用户输入的值。

举个例子，这一项功能会被用在接收**仅用位置无法明确含义**的参数上。比如若有函数`read`定义为`string read(Readable source, bool check)`，第一个参数是读操作的目标，第二个是读取内容时是否检查；则不检查内容，直接读取某个文件(名称为`doc`)的函数长成这样`read(doc, false)`。单看函数调用，几乎没法弄明白为何会有一个`false`在这里。

只允许指名传参也可以防止用户错误地传入一个函数，而忽略了这个函数接受的参数数量(一个例子，JavaScript中的**`map`方法**和**`parseInt`函数**——如果`radix`必须指名传参的话，`parseInt`就无法作为`map`的参数，因为参数数量不符合)。

同时，当函数定义中存在多个**不确定数量**的<u>参数组</u>时，当产生歧义时，某些参数会要求指名传参。比如这个例子:

<div
    style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em; font-size: 14.5px;">
    <span style="color: #0094c8; font-weight: bold;">function</span> <span
        style="color: #2ca9e1;">printInteger</span>(<span style="color: #9ed44c"><b>int...</b></span> <span
        style="color: #e0a37e">ints</span>, <span style="color: #9ed44c"><b>int</b></span> <span
        style="color: #e0a37e">print_num</span>, <span style="color: #9ed44c"><b>int...</b></span> <span
        style="color: #e0a37e">unused_variable</span>)
    <br>
    {<br>
    &nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #bc64a4"><b>for</b></span> (<span
        style="color: #9ed44c"><b>int</b></span> <span style="color: #f39800">i</span> <span
        style="color: #a59aca"><b>in</b> <span style="color: #e95295">0</span><span
            style="color: #a59aca"><b>..</b><span style="color: #e0a37e">print_num</span>)
            { <span style="color: #2ca9e1;">print</span>(<span style="color: #e0a37e">ints</span><span
                style="color: #a59aca"><b>[</b></span><span style="color: #f39800">i</span><span
                style="color: #a59aca"><b>]</b></span>) ; }<br>
            } <br> <br>
            <span style="color: #2ca9e1;">printInteger</span>(<span
                style="text-decoration: red wavy underline 1.2px; text-decoration-skip-ink: auto;"
                title="Missing argument: &quot;int print_num&quot;. You should assign it by its name like &quot;print_num=0&quot;."><span
                    style="color: #e95295">10</span>,
                <span style="color: #e95295">20</span>, <span style="color: #e95295">30</span>, <span
                    style="color: #e95295">2</span>, <span style="color: #e95295">10</span>,
                <span style="color: #e95295">20</span>, <span style="color: #e95295">30</span></span>) ;
</div>

如果不手动指定`print_num`，编译器会无法分辨出哪个<u>实际参数</u>对应哪个<u>声明参数(或参数组)</u>。

### 只允许位置传参

类似地，如果希望使用者必须用`f(0, 3)`这样的形式，而非`f(b=0, a=3)`的形式传递某些参数，则定义函数时，在想要 *只允许位置传参* 的参数**后面**，加上一个**`/`参数**。需要注意的是，只允许位置传参的参数，必须放在参数元组的**最前方**。

举个例子，这一项功能可被用在**不希望用户打乱顺序，进行参数指定**时。

示例:

函数`function int f(int a, /, int b=0, int c)`**允许**这样调用:

* `f(1, 2, 3)` (a=1, b=2, c=3)
* `f(1, c=1)` (a=1, b=0, c=1)
* `f(1, c=3, b=2)` (a=1, b=2, c=3)

<span style="color: #e60033; font-weight: bold">不允许</span>这样调用:

* <del style="color: #e60033">`f(a=1, 2, 3)`</del> (尽管位置正确，但`a`不接受<u>指名传参</u>)
* <del style="color: #e60033">`f(c=3, a=1)`</del> (道理同上，不如说这样写更让人觉得不对了)



## 参数状态限制

**参数状态限制**可用于快速判断函数接收的参数**是否可用于该函数**。要创建它，只需要在参数名后加上冒号，并加上希望的**状态限制子**即可。如果用户以不正确的方式传入参数，编译器会尽可能早地发现这一点，并报出错误阻止用户这样做。

状态限制子有以下几种形式: 类、形容、或是可以被评价为`bool`的语句。

一部分的对参数接受类型的限制(即，要传入的实际参数必须满足的条件)可以后置，一个参数完整的定义像这样`形式参数在函数体内的类型 实际参数必须满足的条件 形式参数名`。全放在前面太乱了，不如作为参数状态限制后置于参数。

可以用`with`从句，将参数的状态限制在参数列表后面写出——这样更美观。

### 修饰符限制子

当希望接受的参数类型只能为某种被修饰符限定的类型时，将那些修饰符置于`:`后方，即可将它们作为限定的一部分。

注意，如果把修饰符放在参数类型前方，代表着“将接受的值进行该修饰后，赋予参数”；如果放在类型后方，则是代表“只可接受具有该修饰的类型”。当然，写`int const a`实在是有些怪，不如把这个`const`当作限制子理解更加自然。

例如，想要制作一个在编译期间就可以算出加法结果的函数，那得要求你的参数必须都是常数才行(还有更简单的方式书写此类函数(链接的PLACEHOLDER)):

<div
    style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em; font-size: 14.5px;">
    <span style="color: #0094c8; font-weight: bold;">function</span> <span
        style="color: #2ca9e1;">addTwoConst</span>(<span style="color: #9ed44c"><b>int</b></span> <span
        style="color: #e0a37e">a</span>: <span style="color: #68be8d"><b>const</b></span>, <span
        style="color: #9ed44c"><b>int</b></span> <span style="color: #e0a37e">b</span>: <span
        style="color: #68be8d"><b>const</b></span>)
    <br>
    {<br>
    &nbsp;&nbsp;&nbsp;&nbsp; <span style="color: #bc64a4"><b>return</b></span> <span style="color: #e0a37e">a</span>
    <span style="color: #a59aca"><b>+</b></span> <span style="color: #e0a37e">b</span>;<br>
    }
</div>

### 类限制子和形容限制子

当需要用多态处理函数，但只希望接收部分子类的实例做参数时，可以采用类限制子。使用`a|b`来代表可以是`a`或`b`类型，使用`a&b`来代表不仅要是`a`且是`b`类型(这可以用在多继承上，比如，设计一个角色食用物品，那么这个物品必须**可食用**并且**没有过期**)。`|`和`&`**可以混用**于**类**和**形容**限制条件都存在时。可以用括号将限制条件包围起来以构造更为复杂的限定。

下面这个例子说明了，接受的参数`a`作为`Animal`传入函数，但要么属于`Cat`类，要么属于`SmallDog`类。

```typescript
function void printCryOf(Animal a: Cat|SmallDog)
{
    print(a.cry());
}
```

### `bool`限制子

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
    at test.my_sqrt() (line 1, ref line 0): < ParamStateCheck >
    at test.main() (line 9, ref line 1): my_sqrt(double(input()))

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

当然，`bool`限制子可以适用于复杂的参数限定。这时，可以用`typeof`来判断参数是否属于某个**类**或是**形容**。比如要求一个参数`a`既属于

## 快速函数制造

下面展示了如何自定义一个<u>不会换行的`print`函数</u>(我们可以叫它`printx`)。

```typescript
let printx = (any... args, string sep=" ", ostream target=stdout) -> print(args, sep, target, end="");
```

观察上面的函数，你会发现除了`end`参数被修改了以外，其余参数和`print`保持一致。这时，我们可以采取`where`关键字来简化我们的工作。

```typescript
let printx = print with end="";
```

也可以同理制作一个打印到标准错误的`printerr`函数

```typescript
let printerr = print with target=stderr;
```
