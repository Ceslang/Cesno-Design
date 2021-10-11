# builtin模块

## 简介

`builtin`模块是Cesno中的内置模块，被每一个Cesno代码文件默认地引入全局命名空间，可以无需额外操作立即使用。该模块提供了编程中最为常用的函数，旨在为编程者书写程序提供便利。

**修饰子**: `public module `。

**本文件适用的版本**: `in-design`。

# 常数列表

## std相关

* `istream stdin = runtime.env.input_stream`

**用途**: 接受来自目前运行环境的标准输入。

* `ostream stdout = runtime.env.output_stream`
* `iostream stdio = runtime.env.io_stream`
* `ostream stderr = runtime.env.error_output`

# 函数列表

## print函数

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



## sort函数



## exit函数

**用途**: 终止程序执行。

**注意**: 在程序运行中任意停止程序运行可能会导致意想不到的结果，包括但不限于 *数据读写失误*、*运算结果丢失*、*干扰相关程序运行* 等意想不到的结果。强烈建议**不要在应该书写`return`语句的地方使用`exit()`代替**。

**函数签名**: `never exit(/, )`
