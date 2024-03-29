# array类

## 简介

**数组**(`array`)属于Cesno中的常用容器类型。它的长度固定，支持**直接访问**(随机访问)。

**包名**: `cesno.type.array`

**修饰子**: `public class`

**泛型列表**: `<type EleType, int length>`

**本文件适用的版本**: `in-design`

# 函数及方法列表

## 构造器

#### `constructor(EleType... elems, /, int capacity)`

## 函数

## `slice`方法

**用途**: 将数组进行切片操作。即给定一段范围，返回原数组处在该范围内的一段。

**参照**: 多数情况下，建议使用更为方便的[`[]`运算符](#operator_bracket)。

**函数签名**: `method EleType[] slice(int start=0, int end)`

## `get`方法

**用途**: 返回数组

## `fill`方法 ==链式返回==

**用途**: 将数组中一段区域填充指定值。如果指定一个可迭代容器，则可指定**循环地填充**或**只按位填充**。

**参照**: 多数情况下，建议使用更为方便的[`[]`运算符](#operator_bracket)。



## `map`方法

**用途**: 将该数组中的元素映射到新容器中。换句话说，就是采用某个转换器，对本数组每个元素做转换，再依次填入到新容器中。

**函数签名**: 
``` c++
method <MappedType, RetContainerType> RetContainerType<MappedType>
map(function<EleType, MappedType> mapper, 
    int from=0, int before=len(self),
    RetContainerType into: Container = self.type)
```

**参数列表**: 

* `mapper`: `function<EleType, MappedType> mapper`

​	接受一个转换器，用于将每个元素转换成需要的内容。比如，如果要把每一个数据加上1，则`mapper`要这样书写: `x.map(e -> e + 1)`。

- `from`: 

* `into`: `RetContainerType into: Container.type&into.type.constructor.check(MappedType)=self.type` ==默认参数==

​	如果需要转换数据同时，改变数据保存到其他容器中，则这里需要提供一个新的类型。比如，如果想把映射过后的数组，转换成辞典型，则应该像这样写: `x.map(someActionWhichProduce2EleTuple, dict)`。

`into`存在两个限制。第一，它必须是一个属于`Container`的**类型**(不能是一个**实例**)。

**示例**:

```c++
int[] a = [1, 2, 3];
print(a.map(e -> e + 1));    // 输出 [2, 3, 4]
print(a.map(e -> 2 * e, range()));    // 输出 [2, 3, 4]
```



## `filter`方法

<div
    style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em; font-size: 14.5px;">
    <span style="color: #0094c8; font-weight: bold;">method</span> <span style="color: #00a381; font-weight: bold;">EleType</span><span style="color: #9ed44c; font-weight: bold;">[]</span> <span style="color: #2ca9e1;">filter</span>(<span style="color: #e0a37e">rule</span>: (<span style="color: #00a381; font-weight: bold;">EleType</span> <span style="color: #e0a37e">e</span>, <span style="color: #9ed44c; font-weight: bold;">integer</span> <span style="color: #e0a37e">index<span style="color: #9ed44c; font-weight: bold;">?</span></span>) <span style="color: #0094c8; font-weight: bold;">-></span> <span style="color: #9ed44c; font-weight: bold;">bool</span>) ;
</div>

## `indexOfFirst`方法

<div
    style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em; font-size: 14.5px;">
    <span style="color: #0094c8; font-weight: bold;">method</span> <span style="color: #9ed44c; font-weight: bold;">int</span> <span style="color: #2ca9e1;">indexOfFirst</span>(<span style="color: #e0a37e">element</span>: <span style="color: #00a381; font-weight: bold;">EleType</span>) ;
</div>

**用途**: 返回数组中第一个`element`的下标。

<div
    style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em; font-size: 14.5px;">
    <span style="color: #0094c8; font-weight: bold;">method</span> <span style="color: #9ed44c; font-weight: bold;">int</span> <span style="color: #2ca9e1;">indexOfFirst</span>(<span style="color: #e0a37e">rule</span>: (<span style="color: #00a381; font-weight: bold;">EleType</span> <span style="color: #e0a37e">e</span>, <span style="color: #9ed44c; font-weight: bold;">integer</span> <span style="color: #e0a37e">index?</span>) <span style="color: #0094c8; font-weight: bold;">-></span> <span style="color: #9ed44c; font-weight: bold;">bool</span>) ;
</div>

**用途**: 返回数组中第一个满足`rule`的元素的下标 (即`rule`判断为真)。

## `indexOfAll`方法

<div
    style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em; font-size: 14.5px;">
    <span style="color: #0094c8; font-weight: bold;">method</span> <span style="color: #9ed44c; font-weight: bold;">int[]</span> <span style="color: #2ca9e1;">indexOfAll</span>(<span style="color: #e0a37e">element</span>: <span style="color: #00a381; font-weight: bold;">EleType</span>) ;
</div>

**用途**: 返回数组中所有`element`的下标。

<div
    style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em; font-size: 14.5px;">
    <span style="color: #0094c8; font-weight: bold;">method</span> <span style="color: #9ed44c; font-weight: bold;">int[]</span> <span style="color: #2ca9e1;">indexOfAll</span>(<span style="color: #e0a37e">rule</span>: (<span style="color: #00a381; font-weight: bold;">EleType</span> <span style="color: #e0a37e">e</span>, <span style="color: #9ed44c; font-weight: bold;">integer</span> <span style="color: #e0a37e">index?</span>) <span style="color: #0094c8; font-weight: bold;">-></span> <span style="color: #9ed44c; font-weight: bold;">bool</span>) ;
</div>

**用途**: 返回数组中所有满足`rule`的元素的下标 (即`rule`判断为真)。


## `reduce`方法

**用途**: 给定某个操作，将其归约到数组中每个元素。换句话说，就是先把数组中前两个元素，用给定方法计算并返回新值，再计算新值和第三个元素的值……以此类推，直到数组结尾。

**注意**: 这里的`reduce`并不是“减少”的意思，而是编程中的“归约”操作。如果你想要寻找 *缩减数组长度* 的“切片”操作，请移步[`slice`方法](#slice方法)。

**函数签名**: `method <FuncRetType> FuncRetType reduce(function<(EleType|FuncRetType, EleType), FuncRetType> reducer)`

**参数列表**:

* `reducer`: `function<(EleType|FuncRetType, EleType), FuncRetType>`

接受一个操作，用于归约地(依次地)应用于数组的每个元素。这个操作**必须接受**两个类型为`EleType`的参数；或一个是`EleType`，另一个是`FuncRetType`的参数。它们的操作返回值类型为`FuncRetType`。

这个操作(`reducer`)可以将数组本身存储的数据的类型，在计算时发生改变(比如从`EleType`改变至新类型`FuncRetType`)，但必须保证改变后的类型，同样能被该操作(`reducer`)进行运算(`FuncRetType`可以被`reducer`作为接受值的类型)。

示例如下。若一个`any[] x`中内容如下`["Student Name", "Bob", "Age", 18, "Gender", Gender.queer]`(`Gender`是一个可被正确转为预期结果的枚举类型(`enum`，此处这个`enum`可正确转为字符串))。若想将这个数组中的内容，全部连接成一个长字符串，并在每一项之间加上空格，则可以这样书写`x.reduce(string::concat(sep=" "))`。因为`string`类中的`concat`函数理论上可以接受任意值，并连接它们，返回成字符串(即可用于下一次连接)。

**示例**:

1. 将一个保存了`bool`类型的数组中，所有元素取`and`运算

```C++
print([true, false, true].reduce(operator::and));    // 返回 false
print(["1", "a", 4].reduce(operator::plus));         // 返回 "1a4"
```



## `sum`方法 ==调用限制==

**用途**: 归约地将加法应用于数组每个元素。换句话说，就是相当于把数组中所有的元素抽出来，在中间写上加号，再计算结果。等价于[`reduce`方法](#reduce方法)的`reduce(operator::add)`。

**调用限制**: `EleType`必须具有`Addable`形容。换句话说，本数组所存储的元素必须可被相加，即都可以被`+`连接并计算。

**函数签名**: `method EleType sum() : EleType kindof Addable`

**示例**:

```java
print([1, 2, 3].sum())                               // 输出 6
print(["1", "2", "4"].map(int.constructor).sum())    // 输出 7
```

# 可用操作符列表

## `+`运算符

**用途**: 连接两个数组，让前一个数组的尾接上后一个数组的头。

**重载**:

1. `self + array<EleType>` returns `array<EleType>`

   **右操作对象**: 存储同样类型的数组`array<EleType>`。

   **返回类型**: `array<EleType>`

2. `self + array<any>` returns `array<any>`

   **右操作对象**: 被标记为动态类型的数组`array<any>`。

   **返回类型**: `array<any>`

## `-`运算符

**用途**: 删去前一个数组中的，出现在后一个数组中的值。类似于数学中的**集合减法**。



## `*`运算符

**用途**: 创造**重复前一个数组的元素**的新数组。

**右操作对象**: 一个整数。`RightType extends int`。

**示例**:

```c++
int[] a = [1, 2] * 3;
print(a)    // 输出 [1, 2, 1, 2, 1, 2]
```



## `&`运算符

**用途**: 

## `|`运算符

**用途**:

## `[]`运算符 ==可修改原实例==

<span id="operator_bracket"></span>

**用途**: 将数组进行切片操作。即给定一段范围，返回原数组处在该范围内的一段。

**参照**: 可以把**`[]`运算符**视作[`slice`方法](#slice方法)的语法糖。

**注意**: 通常下标从0开始计数，但如果你更改了显示设置，请注意所填写的下标是否正确。

**重载**:

1. `[int n]` returns `ref EleType`

   从数组中以下标形式，取出第n个特定的元素。比如从`x`数组中取出第二个元素，就可以书写成`x[2]`。

2. `[range r]` returns `array<ptr EleType>`

   从数组中以下标形式，取出特定范围的一段。比如从`x`数组中取出从第一个(包含)到第三个(不含)元素，就可以这样书写`x[1..3]`。

3. `[any... args: int|range]` returns `array<ptr EleType>`

