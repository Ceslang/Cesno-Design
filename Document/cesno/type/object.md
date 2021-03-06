# object类

## 简介

`object`类是Cesno所有类的基础类，换句话说，所有其他的类型都是`object`的扩张类，它们都默认地`extends object`。

**修饰子**: `public class`

**本文件适用的版本**: `in-design`

# 成员列表



# 函数及方法列表

## `repr`方法

**用途**: 将一个实例以字符串形式表现，用于在**代码调试**及**发生错误**时输出信息。

**注意**: 这个方法不是**转换任意对象为字符串**的方法。

**函数签名**: `method string repr()`

## `hash`方法

**用途**: 获取对象的**散列值**(也被叫做**要约值**、**hash code**或是**哈希值**等)。

**函数签名**: `method int hash()`

**示例**:

```c++
print(object().hash());    // 输出 -1255996616，这个值几乎是随机的
```



# 可用操作符列表

## `===`运算符

**用途**: 这个运算符比较两个对象是否为**同一个**对象。

**注意**: 这个运算符**不是`==`**，因此它并不比较两个对象的**内容是否相等**。

