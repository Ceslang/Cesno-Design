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
   
   open("path", mode=(#binary, #append))
   ```



6. 人性化计划 更多的比较器`comparator`。==think again==

   给出排序函数`sort(obj, method=#quick)`。

   1. 比较**第一个待比较元素**大于**第二个比较元素**的，返回`bool`的选择器。
   2. 返回包含两个`comparable`类型的元组的函数。`compare_method=function(a,b){ return a.n>=b.n; }`

7. “属性”: 是对象的“特征”，随着对象改变而改变，不允许外部对他进行修改，只能读取。`data`，`function/method`ではない。

8. `if`、`while`等`bool`への隐式类型转换用语法糖来解决`ifem()`，`ifne()`。



```typescript
function number add(number a, number b) { return a + b; }

function<(number, number), number> add = (number a, number b) -> { return a + b; };
function add = (number a, number b) -> { return number(a + b); };
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

17. `function`加减法? `(f + g)`相当于`fucntion(x){ return f(x) + g(x); }`(`x -> f(x) + g(x)`)。

18. 变更: `namespace`只可用在包含**声明**或**定义**中。用`codeseg`不加语言名来创建一个即用即扔的代码域。 ==Working==

```go
func add(a int) int
{
    a = 1 + 1
    return a
}
```

```typescript
module adder
{
    namespace std
    {
        function int add(int a)
        {
            a = 1 + 1
            codeseg c++
            {
                cout << "1142857";
            }
            return a;//
        }
    }
}
```
//namespace可以嵌套
//gcc -S <xxx.cpp> ==> xxx.asm
//

```c++
int main()
{
    print(a+b);
    namespace
    {
        // ...
    }

}
```

19. 用户可以用类似于**友元函数**的方式修改一个官方的类，但是修改会被添加到“可能的错误列表”中。 ==本次讨论==

```
"helloworld" + 1234 + 1.1 + null + 'x';
"helloworld" + str(1234) + str(1.1) + str(null) + str('x');  //py

int a, b = 0, 0;
a=a+b //会被解析到下面那种
eval { ADD a, b }
```

```
int a = 0;
String b = "a";
String c = str(a) + b;
eval 
{
    register d, 3;
    a+=30;
    memory[0x1024] = a;
    memory[0x1025] = 67;
    put monitor memory[0x1024:0x1025]
}


operator+ (int right)
{
    eval {  }
}
```

20. 匿名函数学习C++，可以指定**闭包**(翻译提案: 捕获)。

21. 赋值表达式会“返回”值。如果是`=`赋值，返回值；如果是`:=`赋值，返回创建变量的地址(相当于这个变量本身)。

提议：`:=` 用于复制地址

```c++
int a = 0;
print(int b = a + 5);

while ((int c := b) != 0)
{
    // Do something
}

// 1. a == a?
// 2. a == b <=> b == a?
// 3. a == b , b == c ==> a == c?
// 满足这三个才叫相等吧;
// example : 
a = "abc" , b = "ab"+"c"
a != b
a = #FFFFA b = #FFFFB 
a == b? //java "aa" != "a"+"a"
"aa".equals("aa") // true
"aa" == "aa" ==> Object a.equals(Object b) // java

// 近似相等(~=，大部分情况用户自己定义)/相等(值)/强相等(内存块是否为同一个)?
0.09999999999999999999999 ~= 0.1000000000000001?

int c = b;
while (c != 0)
{
    c = random();
    print("Run one time.");
}
```

```c++
int a = 10;
int b := a;
int b = a;
b;
a = 20;
```


23. 对于**修饰子**的摆放位置: 公共修饰子 特殊修饰子 声明或定义。其中，公共修饰子需要把**访问修饰子**放在最前。 ==本次讨论==

    `public inline method int f(int x)`
    
24. 引入命名空间。比如假设某个两个包的名字是`org.example.Pack1`和`org.example.Pack2`: ==本次讨论==

    则引入`org`可以让我们这样书写`org.example.Pack1`,

    引入`org.example`可以写成`example.Pack1`。

25. `for`循环是否OK ==本次讨论==

26. 类型转换提供方法:

当一个类`SomeClass`已经写完后，如果不想修改原类，并让`SomeClass(any obj)`不失效，可以由写一个`cast`提供方法。其实相当于在新类中加入一个方法，然后把所有的`SomeClass(any obj)`改成类似于`inst.toSomeClass()`这种

```c++
class int
{
    // Some code...
    public cast any;    // allow any cast
    // You can also write "public <FromType extends AClass> cast FromType;" to allow only
}

class Test
{
    int data;
    // some code
    
    cast int
    {
        return self.data;
    }
    
    cast float return float(self.data); // 如果 float 没有这种构造器，cast 无效。这样可以避免出现安全性问题
                                        // 其实这个感觉就是个语法糖
}

void main()
{
    int a = 10;
    Test b = Test(10);
    print(a + int(b));    // 打印出 20
    print(1.0 + float(b));    // 打印出 20.0
}
```

