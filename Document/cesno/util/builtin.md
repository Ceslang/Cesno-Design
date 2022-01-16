# builtin模块

## 简介

`builtin`模块是Cesno中的内置模块，被每一个Cesno代码文件默认地引入全局命名空间，可以无需额外操作立即使用。该模块提供了编程中最为常用的函数，旨在为编程者书写程序提供便利。

**修饰子**: `public module `

**本文件适用的版本**: `in-design`

# 常数列表

## std相关

* `istream stdin = runtime.env.input_stream`

**用途**: 接受来自目前运行环境的标准输入。

* `ostream stdout = runtime.env.output_stream`
* `iostream stdio = runtime.env.io_stream`
* `ostream stderr = runtime.env.error_output`



# 类型列表

## `int`

**简介**: (中)整数型，类似于C++或Java的`int`，长32位，范围为-2147483648至2147483647。

**定义**: `type int = cesno.type.integer<32>`

## `long`

**简介**: 长整数型，类似于C++或Java的`long`，长64位，范围为-18446744073709551616至18446744073709551615。

**定义**: `type long = cesno.type.integer<64>`

## `float`

**简介**: 浮点型，类似于C++或Java的`double`，双精度。

**定义**: `type float = cesno.type.fltdeci<64>`

## `bool`

## `char`

## `string`

## `object`





# 函数列表

## `print`函数

**用途**: 将指定到`objs`的任意类型的参数，输出至指定标准输出流。这个函数通常被用作*在控制台显示文本*。

**函数签名**: `function void print(any... objs, ostream target=stdout, string sep=" ", string end="\n")`

**参数列表**: 

* `any... objs`

接受任意类型的输入，并将这些类型转换为可供`ostream`输出的形式。一般地，当`target`接受默认输出流`stdout`时，`objs`中的元素将会被逐层转换成`string`。

* `ostream target=stdout`

`print`函数的输出目标，默认输出到`stdout`。

* `string sep=" "`
* `string end="\n"`

**示例**: 

1. 输出字符串`"Hallo Walt."`到控制台

```python
print("Hallo Walt.");
```

2. 把数字`65535`输出到和该Cesno代码文件同级的`test.txt`中

```lua
print(2 ^ 16 - 1, target=ostream(file("./test.txt", mode=#write)));
```



## `sort`函数



## `exit`函数

**用途**: 强制终止程序执行，不做任何收尾工作。Cesno会在控制台报告一条警告信息，来表示这个程序并非正常退出。

**注意**: 在程序运行之时，强制地停止程序可能会导致意想不到的结果，包括但不限于 *数据读写失误*、*运算结果丢失*、*干扰相关程序运行* 等意想不到的结果。强烈建议**<span style="color: #e60033">不要</span>在应该书写`return`语句的地方使用`exit()`代替**。

**函数签名**: `never exit()`



## `random`函数

**用途**: 生成一个在$[\mathtt{start},\mathtt{end})$之间的`float`型的随机数。

**注意**: 若想要生成整数，请参考[`randint`函数](#randint函数)。

**函数签名**: `float random(float start=0.0, float end=1.0, enum mode=#normal)`



## `randint`函数

**用途**: 生成一个在指定范围内的`int`型的随机数。
