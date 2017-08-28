---
title: javascript 引用类型、原始数据类型值作为参数在函数传递中的机制
---
在javascript中一个变量可以存放两种类型的值，基本类型的值（primitive values）和引用类型的值（reference values）
### 基本类型
也叫原始数据类型，JavaScript 中的基本数据类型有：Undefined、Null、Boolean、Number、String、Symbol (new in ES 6)
### 引用类型
除过上面的基本数据类型外，剩下的就是引用类型了，统称为 Object 类型。细分的话，有：Object 类型、Array 类型、Date 类型、RegExp 类型、Function 类型 等
### 这两种数据类型作为参数在函数传递方式是什么？
我们来了解下几种函数传参调用方式
#### 1.传值调用（Call-ny-value）
所谓传值调用是指传递给函数参数是函数被调用时所传实参的拷贝。在传值调用中实际参数被求值，其值被绑定到函数中对应的变量上（通常是把值复制到新内存区域）
#### 2.引用调用（Call-by-reference）
所谓引用传递是指在调用函数时将实际参数的地址传递到函数中，那么在函数中对参数所进行的修改，将影响到实际参数。
```
function changeStuff(a, b, c)
{
  a = a * 10;
  b.item = "changed";
  c = {item: "changed"};
}

var num = 10;
var obj1 = {item: "unchanged"};
var obj2 = {item: "unchanged"};

changeStuff(num, obj1, obj2);

console.log(num);  //10
console.log(obj1.item); // "changed"
console.log(obj2.item); // "unchanged"
```
从上面这段代码可以看出来，基本数据类型是按值传递，而引用类型传递方式怎么理解？假如引用类型为按引用传递obj1确实受函数内部影响改变了值，但为什么obj2没有改变？
####  3.共享调用
在javascript中引用类型的传递方式实际为传共享调用(call-by-shareing)。传共享调用和传引用调用的不同之处是，该求值策略传递给函数的参数是对象的引用的拷贝，即对象变量指针的拷贝。

### 结论
函数传参在对象类型的情况下，变量值是地址，而不是对象结构本身。将一个变量分配给另一个变量 - 复制其值引用;因此两个变量都引用了内存中相同的位置。新值（新地址）的下一个任务解除绑定从旧地址的名称，并结合新的
对象地址。
