写在前面
================

这里是Ozelot。一个正在学习编程，希望和各位大佬一起交流学习的大学生。这是我们设计团队关于编程语言Cesno的**设计方案**，欢迎大家评论交流!

提示: 最终设计尚未决定，可能还有很多设计上的不足需要优化，故内容可能会发生变动。因为没法不加标签，我不得不打了“程序员”标签。希望没有给大家造成困扰。

注意: 因为Cesno并未制作完成，这里只记录Cesno的语法规范。正因如此，代码部分的高亮可能不能保证每一次都正确显示。如果影响了阅读，我感到十分抱歉!

----


条件与选择
================

## 条件式

**条件式**(condition)是任何可以返回<u>真伪值</u>的表达式，可以嵌套。

## 选择结构

当你不希望你的代码只从上至下地执行时，可以采用选择结构。它可以在某些情况下，跳过某一部分代码，就像人类根据不同情况做出选择。

# if结构

## 基本结构

* if和elif(else if)后，必须且只能接受一个条件式和一个代码块。代码块为空会报出警告。
* if自上而下地判断，当一个条件式为真时，会立即执行对应代码块，并在之后跳过判断之后的条件式以及执行它们对应的代码块。
  * 小提示: 可以书写单一的if语句，如果你需要判断每个条件式。

* else后，必须且只能接受一个代码块。
* if结构有评价值，为其执行的代码块的评价值(如无，则默认为代码块最后一句语句的评价值)。

### 单一的if语句

<div style="font-family: 'Ubuntu Mono'; line-height: 1.4em;">
<span style="color: #bc64a4; font-weight: bold">if</span> <b>(</b><span style="color: #c5c56a;">conditions</span><b>)</b>
<b>{</b> <span style="color: #c5c56a;">code_segment</span> <b>}</b>
</div>


注: <b>粗体字</b>部分是表示需要书写内容本身(比如<b>if</b>表示这里就是写`if`本身) (这里记入的是标准交换格式的Cesno，所以部分括号也被标记成了粗体)，而正常粗细的部分表示“说明性质的内容”(比如condition表示一个条件式)。<i>斜体字</i>部分为可以省略，也不会导致语法出错的部分。

### if和处理其他情况的else

<div style="font-family: 'Ubuntu Mono'; line-height: 1.4em;">
<span style="color: #bc64a4; font-weight: bold">if</span> <b>(</b><span style="color: #c5c56a;">conditions</span><b>)</b>
<b>{</b> <span style="color: #c5c56a;">code_segment</span> <b>}</b><br>
<span style="color: #bc64a4; font-weight: bold">else</span> <b>{</b> <span style="color: #c5c56a;">code_segment</span> <b>}</b>
</div>

### <div style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em">
    <span style="color: #2ca9e1">input</span>();
    <span></span>
</div>

### if结构的语法

<div style="font-family: 'Consolas'; line-height: 1.4em;">
<span style="color: #bc64a4; font-weight: bold">if</span> <b>(</b><span style="color: #c5c56a;">conditions_1</span><b>)</b>
<b>{</b> <span style="color: #c5c56a;">code_segment_if_1_true</span> <b>}</b><br>
<i><span style="color: #bc64a4; font-weight: bold">elif</span> <b>(</b><span style="color: #c5c56a;">conditions_2</span><b>)</b>
<b>{</b> <span style="color: #c5c56a;">code_segment_if_2_true</span> <b>}</b><br>...<br>
<i><span style="color: #bc64a4; font-weight: bold">elif</span> <b>(</b><span style="color: #c5c56a;">conditions_n</span><b>)</b>
<b>{</b> <span style="color: #c5c56a;">code_segment_if_n_true</span> <b>}</b><br>
<span style="color: #bc64a4; font-weight: bold">else</span> <b>{</b> <span style="color: #c5c56a;">code_segment_for_all_if_and_elif_are_false</span> <b>}</b></i>
</div>
# match结构

* match需要接受一个被括号包围的、拥有评价值的部件(记为a)，和一个用于match的代码块。
* 用于match的代码块中，如果没有涵盖a能出现的所有情况，则会报出警告。
* 为了添加一个处理分支，首先写出期望的a的值；如有多个期望值，可用逗号隔开(如有歧义，可加括号解决)。其次，写出双箭头符号`=>`，再写一个代码块。
  * 小提示: 单独的一个字符串或是数字等，都是一个语句；而当代码块只有一个语句时，多半可以省略环绕的大括号。所以有些情况，可以直接省去书写大括号。
  * 双箭头符号的意思是“扩展”或“替换”，拥有一些更加接近元编程的用法。请不要和单箭头符号(多半代表闭包)混淆。
* match结构有评价值，为其执行的代码块的评价值。

### 利用match结构

输入一个整数，如果是4，则给变量s赋值字符串"it is four"，1或3则为"it is one or three"，其余情况则赋值为"others"。

<div style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em">
    <span style="color: #9ed44c"><b>string</b></span> <span style="color: #f39800">s</span>
    <span style="color: #A59ACA; font-weight: bolder;">=</span>
    <span style="color: #bc64a4; font-weight: bold">match</span>
    (<span style="color: #9ed44c; font-weight: bold">int</span>(<span style="color: #2ca9e1">input</span>())) { <br>
    &nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #E95295">4</span>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b style="color: #bc64a4; font-weight: bold">=></b>
    "<span style="color: #98623C">it is four</span>" ;<br>
    &nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #E95295">1</span>, <span style="color: #E95295">3</span>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b style="color: #bc64a4;">=></b>
    "<span style="color: #98623C">it is one or three</span>" ;<br>
    &nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #bc64a4; font-weight: bold;">otherwise => </span>
    "<span style="color: #98623C">others</span>" ;<br>
    };
</div>


### match结构的语法

<div style="font-family: 'Consolas'; line-height: 1.4em;">
    <span style="color: #bc64a4; font-weight: bold">match</span> <b>(</b><span style="color: #c5c56a;">statement</span><b>)</b><br>
    <b>{</b><br>
    <i>
        &nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #c5c56a;">different_result_to_different_code</span> <br>
    </i>
    <b>}</b>
</div>

对于有内容的match结构来说:

<div style="font-family: 'Consolas'; line-height: 1.4em;">
    <span style="color: #bc64a4; font-weight: bold">match</span> <b>(</b><span style="color: #c5c56a;">statement</span><b>)</b><br>
    <b>{</b><br>
    &nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #c5c56a;">result_1<i><span style="color: #000"><b>, </b></span> result_2<span style="color: #000"><b>, ..., </b></span>result_n</span></i>
    <b style="color: #bc64a4; font-weight: bold">=></b> </b><span style="color: #c5c56a;">value_or_code_seg_if_statement_is_in_result_1_to_n</span> <b>;</b> <br>
    <i>
        &nbsp;&nbsp;&nbsp;&nbsp;<span style="color: #bc64a4; font-weight: bold;">otherwise => </span>
        <span style="color: #c5c56a;">value_or_code_seg_if_statement_value_not_in_given_result</span>
    </i><b>;</b> <br>
    <b>}</b>
</div>
