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
10. 方法调用限制: 某些方法在该对象满足特定条件时才可以被调用 ==(Working)==
    1. 优点: 使滥用`object`类型创建方法的现象更少
    2. 缺点: 对动态类型支持较差
11. 容器方面大括号中括号小括号满天飞，容易给用户造成困扰。
    这里讨论的都是**字面量**，代码块除外。
    * 小括号代表元组`tuple`。
    * 中括号代表数组`array`。
    * 大括号:
      * 匿名对象`@{a: 10, b: "a"}`
        * `class { public int a; public string b }.constructor(10, "a")`
      * 由**逗号分割**的项目(们): 集合`set`。
      * 由**逗号分割**的项目，至少**有一个有冒号**: 辞典`dict`。如果有其它项没有冒号，会警告。
      * 至少有一个是**由分号分割**的项目: 代码块`codeseg`。
12. `a, b = b, a`问题

`(a, b) = (date(), 1)`

`(a, b) = (b, a)`

`(b, a)` 算出来，整体赋值给 `(a, b)`

`a, b = 1, 10`

13. Cesno形容 (支持多继承情况下的面向对象接口)。

14. 加入复数、矩阵类型 ==(Working)==

15. 运行时的对类(原型)修改 ==to be discussed==

    目前想到的方案。默认是不可通过type来改(也可以提高一些可读性了)

    1.  对所有类型变量`x`，`x.type`内的成员修改不可行。
    2.  对标记为`volatile`的类型的变量`x`，`x.proto`(也可以写`x.class`)内的成员可以修改。
    
    ```c++
    volatile class test
    {
        int x;
    }
    
    test t = test();
    t.x = 1;
    ```
     
    
    
16. **参数直接变换**和**只接受修饰过的参数** ==Working==

    对于函数`function any f(any a)`

    1. 如果是类似`const any a`，则代表**接收到的参数会自动转为常数**。
    2. 如果是类似`any const a`，则代表**只能接受常数**。
    
    使用例:
    对于运算符重载


    
17. `function`加减法? `(f + g)`相当于`fucntion(x){ return f(x) + g(x); }`(`x -> f(x) + g(x)`)。 ==本次讨论==

18. `this` `self`不同用法: `this`是当前环境，`self`是面向对象的“自身”。 ==本次讨论==

19. 变更: `namespace`只可用在包含**声明**或**定义**中。用`codeseg`不加语言名来创建一个即用即扔的代码域。 ==本次讨论==

20. 用户可以用类似于**友元函数**的方式修改一个官方的类，但是修改会被添加到“可能的错误列表”中。

21. 匿名函数学习C++，可以指定**闭包**。

