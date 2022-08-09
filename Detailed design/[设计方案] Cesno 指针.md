# 指针的基础



# 指针的表达

## 永远指向一个对象

当希望一个指针不可改变**其所指向的对象**时，可以使用`const`来定义该指针。

<div style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #FBFAF5; padding: 0.5em 1em">
    <span style="color: #68be8d"><b>const</b></span>
    <span style="color: #9ed44c"><b>ptr</b></span>
    <span style="color: #f39800">pointer_ever_to_one_instance</span>
    <span style="color: #a59aca; font-weight: bolder;">=</span>
    <span style="color: #a59aca"><b>ref</b></span>
    <span style="color: #f39800">some_instance</span>
    ; <br />
    <span style="color: #9ed44c"><b>const</b></span>
    <span style="color: #f39800">pointer_ever_to_one_instance_1</span>
    <span style="color: #a59aca; font-weight: bolder;">=</span>
    <span style="color: #a59aca"><b>ref</b></span>
    <span style="color: #f39800">some_instance</span>
    ; <br />
</div>


## 只读的指针

如果希望指针**只能读取被指向的量**，可以使用泛型，传入`const`作为类型限制。

<div style="font-family: 'Consolas'; line-height: 1.4em; color: #777; background-color: #fbfaf5; padding: 0.5em 1em">
    <span style="color: #9ed44c"><b>ptr</b></span>&lt;<span style="color: #68be8d"><b>const</b></span>
    <span style="color: #9ed44c"><b>int</b></span>&gt;
    <span style="color: #f39800">pointer_to_constant</span>
    <span style="color: #a59aca; font-weight: bolder;">=</span>
    <span style="color: #a59aca"><b>ref</b></span>
    <span style="color: #f39800">some_int</span>
    ; <br />
    <span style="color: #9ed44c"><b>ptr</b></span>&lt;<span style="color: #68be8d"><b>const</b></span>&gt;
    <span style="color: #f39800">pointer_to_constant_1</span>
    <span style="color: #a59aca; font-weight: bolder;">=</span>
    <span style="color: #a59aca"><b>ref</b></span>
    <span style="color: #f39800">some_variable</span>
    ;
</div>
