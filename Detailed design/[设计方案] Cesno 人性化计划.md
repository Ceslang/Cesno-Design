写在前面
================

这里是Ozelot。一个正在学习编程，希望和各位大佬一起交流学习的大学生。这是我们设计团队关于编程语言Cesno的**设计方案**，欢迎大家评论交流!

提示: 最终设计尚未决定，可能还有很多设计上的不足需要优化，故内容可能会发生变动。因为没法不加标签，我不得不打了“程序员”标签。希望没有给大家造成困扰。

注意: 因为Cesno并未制作完成，这里只记录Cesno的语法规范。正因如此，代码部分的高亮可能不能保证每一次都正确显示。如果影响了阅读，我感到十分抱歉!

----



* 给Cesno加入一个`template`文件夹，方便用户复制再加工。
* 进行乘除算(或其他可能的运算)2次幂数时，自动转为**位运算**。
* 自带的教程以及使用帮助。当按下某个按键组合后，可以打开对话框，让用户根据条件，选择合适的代码部件(比如该选择哪一种容器)。
* 允许使用@overload文档注释，来省去大量重复文档注释。

```typescript
/**
 * {@OverloadRoot 
 *     Universal for all overload function doc.
 * }
 * Specific comment for this function.
 */
function void test() { }

/** 
 * {@OverloadDoc}
 * Specific for this function. Different from {@link test()}
 */
function void test(int a) { }
```

* 学学rust的错误报告

```
$ cesno param_state_check_unpass_example.ces --detailed-error-report

Error occured at 01.03.2022 09:26:38 (UTC +08:00).
ParamStateError: -2 is not eligible for parameter state "x >= 0"

~/cesno/param_state_check_unpass_example.ces
------ main function -------------------------------------------
    |
  9 |  my_sqrt(double(input()));
    |          ^^^^^^^^^^^^^^^ Required param x that "x >= 0".
    |                          Got -2.
----------------------------------------------------------------
 
Detailed Report for ParamStateError:
  The parameter for function double my_sqrt(double) has parameter restriction,
  however the input parameter does not fulfill it.

  ~/cesno/param_state_check_unpass_example.ces
  ------ my_sqrt definition --------------------------------------
     |
   1 |  function my_sqrt(x: x >= 0) { return sqrt(x); }
     |                      ------ Param state required here
  ----------------------------------------------------------------
 
  Possible solution:
     Value is received by input() function. Change the input value may solve this problem.
     try: replace line 1 at test.main() to the following statement:
         my_sqrt(double(input("Input one x (double) that satisfy \"x >= 0\": ")));
```

