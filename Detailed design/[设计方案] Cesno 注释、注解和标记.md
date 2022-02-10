写在前面
================

这里是Ozelot。一个正在学习编程，希望和各位大佬一起交流学习的大学生。这是我们设计团队关于编程语言Cesno的**设计方案**，欢迎大家评论交流!

提示: 最终设计尚未决定，可能还有很多设计上的不足需要优化，故内容可能会发生变动。因为没法不加标签，我不得不打了“程序员”标签。希望没有给大家造成困扰。

注意: 因为Cesno并未制作完成，这里只记录Cesno的语法规范。正因如此，代码部分的高亮可能不能保证每一次都正确显示。如果影响了阅读，我感到十分抱歉!

----

这些是什么
================

注释、注解和标记是

注释
================

Cesno有两种注释，而且和其它的语言大同小异: 一种是通常注释，另一种是文档注释。注释可以帮助看到代码的人更好地理解作者的意图。注释在编译时会被编译器忽略。

通常注释
----------------

通常注释包含了**行尾注释**(或“**行内注释**”)和**范围注释**。

行尾注释由“//”开始，到一个(文件意义上的)换行符结束。

```c++
int a = 10;    // 这就是一条行尾注释
               // 你可能已经在别的地方见过多次了
```

范围注释由“/\*”开始，到“\*/”结束，中间可以包含任意内容。

```c++
int a = 10;
/*
从这里
int not_declared_here = 10;
到这里
都是注释
*/
print(a);
```

文档注释
----------------

文档注释是写在定义前的说明性文字，它可以帮助他人快速理解源码。很多代码编辑软件都提供了对文档注释较好的支持。

比如，现有如下一段函数，它的作用是计算两个数字的和:

<div style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em; font-size: 14.5px;">
    <span style="color: #b3ada0">/**<br>&nbsp;* Calculate two number's add. <br>&nbsp;* This function is only for
        demostration.<br>&nbsp;* It is not suggested to write &lt;i&gt;type information&lt;/i&gt; of arguments like
        this.<br>&nbsp;* <br>&nbsp;*
        <b>@constraint</b>(<span style="color: #e0a37e">left</span>, <span style="color: #e0a37e">right</span>) Must be
        a number, which have defined operator plus<br>&nbsp;*
<b>@return</b>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The
        sum of left and right <br>&nbsp;*/</span> <br>
    <span style="color: #0094c8; font-weight: bold;">function</span>
    <span style="color: #2ca9e1;">sumTwoNumber</span>(<span style="color: #9ed44c; font-weight: bold;">any</span> <span
        style="color: #e0a37e">left</span><b>:</b> <span style="color: #9ed44c; font-weight: bold;">number</span>, <span
        style="color: #9ed44c; font-weight: bold;">any</span> <span style="color: #e0a37e">right</span><b>:</b> <span
        style="color: #9ed44c; font-weight: bold;">number</span>) <br>{ <br>
    &nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #bc64a4; font-weight: bold;">return</span>
    <span style="color: #e0a37e">left</span> <span style="color: #a59aca; font-weight: bold;">+</span> <span
        style="color: #e0a37e">right</span>; <br> }
</div>


为了方便可能使用这个函数的人更好地调用它，书写这个函数的人可以提供一段<u>说明性质的文字</u>于<u>文档注释</u>中。

文档注释支持使用HTML标签，这样在导出或查看时，可以提供更多的样式。



### 

注释的妙用
----------------

1. 有时可能需要将代码中的一部分“暂时失效”，这时便可以采用注释的方法使这些代码不会被编译——这种方法被称为“注释掉”。

注解
================

标记
================

标记的作用是对接下来出现的语句进行一定的修饰。