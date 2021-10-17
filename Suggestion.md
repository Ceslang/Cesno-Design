# 今天的讨论🙂

1. 如何不用`SomeClass&`或是`SomeClass*`来表达区分**值传递**和**地址传递**。==to be discussed==

   * 目标: 区分**值传递**和**引用传递**，并采用一致的形式来表示。

   * 建议: 1. 值传递使用比引用传递多

   * 方法: `SomeClassInstance.ptr`。



2. 如何在不区分**基础类型**和**引用类型**的前提下，让`int`、`float`等高效率。==to be discussed==

3. 约等于比较: `~=`。用于提供宽松的比较机制。==(Working)==

   * 存在场景: 用户自定义，`object`中并不包括。

4. 预定义属性。比如`globals`是一个存放了全局变量的词典，`a.datas`代表实例`a`所拥有的数据的字典(可能会有`undefined`值)。==to be discussed==

5. 函数参数枚举: 避免用字符串传入参数，用`#`代表一个参数枚举 ==to be rectify==

   ```
   function void <EleType> sort(EleType obj: sortable, /,  comparator<EleType> #method) //传一个comparator也OK
   {
       enum method {quick(algo.sortQuick), barrel(algo.sortBarrel)};
       obj = method(obj);
   }

   function file open(string path, #mode...) // 只支持了使用内部的enum

   open("path", mode=(binary, append))
   ```



6. 人性化计划 更多的比较器`comparator`。==think again==

   给出排序函数`sort(obj, method=#quick)`。

   1. 比较**第一个待比较元素**大于**第二个比较元素**的，返回`bool`的选择器。
   2. 返回包含两个`comparable`类型的元组的函数。`compare_method=function(a,b){ return a.n>=b.n; }`

7. “属性”: 是对象的“特征”，随着对象改变而改变，不允许外部对他进行修改，只能读取。`data`，`function/method`ではない。

8. `if`、`while`等`bool`への隐式类型转换用语法糖来解决`ifem()`，`ifne()`。



```
function number add(number a, number b) { return a + b; }

function<(number, number), number> add = (number a, number b) -> { return a + b; };
function add = (number a, number b) -> { return a + b; };
function<(number, number), number> add = (a, b) -> { return a + b; };
```



9. 函数参数那一块==歧义==太多了。**重载**和**参数限制并用**不好好设计就会有bug。==think again==
10. 方法调用限制: 某些方法在该对象满足特定条件时才可以被调用 ==(Woking)==
    1. 优点: 使滥用`object`类型创建方法的现象更少
    2. 缺点: 对动态类型支持较差
11. 容器方面大括号中括号小括号满天飞，容易给用户造成困扰。==本次讨论==
    这里讨论的都是字面量，代码块除外。
    * 小括号代表元组`tuple`。
    * 中括号代表数组`array`。
    * 大括号:
      * 匿名对象`@{a: 10, b: "a"}`
        * `class
       { public int a; public string b }.constructor(10, "a")`
      * 由逗号分割的项目(们): 集合`set`。
      * 由逗号分割的项目，至少有一个有冒号: 辞典`dict`。
      * 至少有一个是由分号分割的项目: 代码块`codeseg`。
12. `a, b = b, a`问题 ==本次讨论==

`(a, b) = (date(), 1)`

`(a, b) = (b, a)`

`(b, a)` 算出来，整体赋值给 `(a, b)`

`a, b = 1, 10`

1.  Cesno形容 (支持多继承情况下的面向对象接口)。
2.  加入复数、矩阵类型