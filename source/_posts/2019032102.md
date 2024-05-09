---
title: javascript(二)
date: 2019-03-21 16:43:47
tags:
categories: JavaScript
---
## 元素获取的其他方法
- **1.document.querySelector('Css Selector');**
> 接收一个css选择器（通配，群组，包含，id，类...等等

【注意：如果这个选择器对应的是一组元素，就只找到第0个。】
<!-- more -->

```
var box = document.querySelector('.box');//第一个
var box = document.querySelector('.box:last-of-type');//最后一个
box.style.background = "red"; 
```
- **2.父级.querySelectorAll('Css选择器');**
- 获取元素下某个类型的标签
- 获取结果是一种元素

【注意：一组元素不能在js直接操作,需要添加下标】

- **3.父级.getElementsByTagName('标签名');**
- 获取元素下某个类型的标签
- 获取结果是一种元素
- **4.document.getElementsClassName('Class名');**
- 获取元素下某个类型的标签
- 获取结果是一种元素

- **解：一组元素（元素集合，类数组）**
- 1. 一组元素不能直接操作
- 2. 一组元素哪怕只有一个，它也是一组元素。
- 3. 一组元素在操作的时候，可以使用下标。
- 4. 如果需要知道这组元素有几个，可以使用 length属性

## if语法
>一种操作下会有两种或者以上的执行结果，记得用判断。

```
if(条件){
条件成立的时候需要执行的代码
}

if(条件){
条件成立的时候需要执行的代码
}else{
条件不成立的时候需要执行代码
}

if(条件一){
条件一成立的时候需要执行的代码
}else if(条件二){
条件二成立的时候需要执行的代码
}
....else{
以上条件都不成立的时候执行的代码
}
```
【style提取的是行间样式，所以不建议大家直接使用style里的内容当作判断条件】

## 运算符
- 逻辑运算符
- “==” 等于
- “!=” 不等于
- “>=” 大于等于
- “<=” 小于等于
- “<” 小于
- “<” 大于

## 数据类型
为了能够更方便的描述和使用，程序通常会把要操作的数据，根据其特性，分成不同的类型进行操作。
在javascript中，数据一共可以分成如下七种类型：
1. 简单类型（值）
```
1. Number
由0-9组成的值，还有几个比较特殊的值
a. NaN ->Not a Number
b. Infinity-> 无穷的
2. String
由一对单引号或双引号包含的内容【单引号双引号需要成对】
3. Booleans
用来描述逻辑的真假的，这种类型有且仅有两个值
a. true 表示真
b. false 表示假
【js严格比较大小写字母】
var a = true;
a = !a;//a = false;
var a = false;
a = !a;//a = true;
4. Null
用来描述空值，这种类型有且仅有一个值【注意：当我们使用typeof的时候，返回的是‘object’】
5. Undefined
用来描述不存在的值，这种类型有且仅有一个值
6. Symbol
7. function(){} function函数
```
2. 复杂类型（复合类型、引用类型）
- object：由7种数据类型组合的类型，object中包含7种类型中的任意类型。


## for循环
1. var i = 0;
2. i < li.length;
3. 执行里面面的操作;
4. i++;

**易混解析：**
```
for(var i = 0; i < li.length; i++){
//循环在页面加载完成之后就执行了
li[i].onclick = function(){
/*
*点击li时执行
*这会循环肯定已经执行完了，
*所以在获取i的时候，是循环执行完之后的结果
*/
alert(i);
}
}

```

## this
>在事件函数中this代表触发当前事件的元素

```
for(var i = 0; i < li.length; i++) {
li[i].onclick = function(){
console.log(this,this.innerHTML);
//结果是<span>1111</span>  1111
// 在事件函数中，this代表触发当前事件的元素
};
}
```
## 作业
```
总共有5张图片，src分别为1.jpg,2.jpg,3.jpg,4.jpg,5.jpg
点击 上一张 切换至 上一张图 如果已经是最开始1张 不做任何操作
点击 下一张 切换至 下一张图
如果已经是最后1张 不做任何操作
```
