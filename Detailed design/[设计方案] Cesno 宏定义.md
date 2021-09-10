宏是什么
================

计算机科学里的宏是一种抽象（Abstraction），它根据一系列预定义的规则替换一定的文本模式。解释器或编译器在遇到宏时会自动进行这一模式替换。对于编译语言，宏展开在编译时发生，进行宏展开的工具常被称为宏展开器。

Ref: https://baike.baidu.com/item/%E5%AE%8F/2648286

Cesno 的宏
================

运行宏
----------------

Cesno 的宏分为 define 和 typedef，前者允许用户定义一个标识符为一个字符串（里面允许有参数）；后者允许用户将一个字符串定义为一个数据类型。例如：

```c++
define mian main                                  // 将全文的 mian 替换为 main

define rep(i, a, b) for(int i = a; i <= b; ++ i)  // 将全文的 rep(i, a, b) 替换为
                                                  // for(int i = a; i <= b; ++ i)

                                                  // 此时里面的 a, b 都是数值。
                                                  // 例如，调用 rep(i, 1, n) 那么就会
                                                  // 替换为 for(int i = 1; i <= n; ++ i)

typedef myPair pair<int, pair<int, char>>         // 将 pair<int, pair<int, char>> 类型替换为
                                                  // myPair 类型（仅仅替换数据类型）
                                                  // 也就是说，代码其余的 myPair 不会被替换
```

编译宏
----------------

在 Cesno 编译的过程中，你可以选择在编译选项加上 `-- YOUR-OPTION`，使得源代码的以下内容被执行：

```c++
ifdef YOUR-OPTION {
    //Your Code here..
}
```

例如，源代码如下。

```c++
int a = 10, b = 20;

ifdef cesno {
    a = 20;
}

void main() {
    print(a + b);
}
```

当加入了 `--cesno` 的编译选项的时候，输出是 40，否则输出为 30。
