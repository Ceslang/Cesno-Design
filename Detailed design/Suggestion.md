1. 如何不用`SomeClass&`或是`SomeClass*`来表达区分值传递和地址传递。

2. 如何在不区分**基础类型**和**引用类型**的前提下，让`int`、`float`等高效率。

3. 约等于比较: `~=`。用于提供宽松的比较机制。

4. 预定义属性。比如`globals`是一个存放了全局变量的词典，`a.datas`代表实例`a`所拥有的数据的字典(可能会有`undefined`值)。

5. 函数参数枚举: 避免用字符串传入参数，用`#`代表一个参数枚举

   ```
   function void <EleType> sort(EleType obj: sortable, /,  comparator<EleType> #method)
   {
       enum method {quick(algo.sortQuick), barrel(algo.sortBarrel)};
       obj = method(obj);
   }
   ```

   

6. 人性化计划 更多的比较器`comparator`。

   给出排序函数`sort(obj, method=#quick)`。

   1. 比较**第一个待比较元素**大于**第二个比较元素**的，返回`bool`的选择器。
   2. 返回包含两个`comparable`类型的元组的函数。

