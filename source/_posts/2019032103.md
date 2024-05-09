---
title: javascript(九)
date: 2019-03-21 16:43:54
tags:
categories: JavaScript
---
## 运算符
- 1.赋值运算符
- =、+=、-=、*=、/=、%=
- 2.算数运算符：运算符都只有数字运算的功能，所以在使用的时候，都会把其他类型专程数字。
- "+"
- 1.当加号左右两侧有一位是字符串时，会把另外一侧也转成字符串
- 2.使用+号时，两边没有字符串时，优先尝试把左右两侧都转成数字，如果不能转换成数字就转换成字符串进行链接。
- "-"
- "*"
- "/"
- "%"：取模等于求余数【任何数%n = (0 ~ n-1)】
- ++
- “--”
- 注意：
<!-- more -->

```
var i = 0;
alert(i++); //0
alert(i); //1

var j = 0;
j++;
alert(j);//1
```
- 3.关系运算符
- "<"、">"、"<="、">="、==、!=、===、"!=="
- ->扩展：
- == 和 "==="，以及!= 和!==的区别。
- "==" 和 !=：会进行隐式类型转换，把左右两侧的数据类型转换成一个的之后，再去比较。
- === 和!==：进行比较的时候，也会比较数据类型，数据类型不一样不会进行比较，则判定两边不相等。
- 4.逻辑运算符
- ||：当第一个条件返回true，就结束运行，返回true，如果第一个条件返回false，那再来看第二个条件，如果第二个条件返回true，整体也为true，如果两个条件都为false，则返回false。

- &&：当第一个条件返回false，就结束运算，直接返回false。如果第一个条件返回true，那再来看第二个条件，如果第二个条件返回false，整体也返回false，如果两个条件都返回true则返回true；
- ！：否、取反，把当前的值转换成布尔值，然后取反，返回的结果是布尔值
```
//条件成立，执行某件事
var a = 0;
var b = 2;
function fn(){
alert(1);
}
(a<b) && fn();

//条件不成立，执行某件事
(a > b)||fn();
if(a > b) {

} else {
fn();
}
```

- 5.三元运算符
> 判断条件？成立执行的语句:不成立执行的语句

- 条件成立返回：成立执行的结果
- 条件不成立返回：不成立执行的结果 
```
var a = 10;
var b = 12;
var c = a > b ? a:b;


eg:
window.onload = function() {
var btn = document.querySelector('input');
var box = document.querySelector('#box');
var isHide = true;
btn.onclick = function(){
/*if(isHide) {
box.style.display = "block";
} else {
box.style.display = "none";
}*/
//box.style.display = isHide?"block":"none";
isHide?box.style.display = "block":box.style.display = "none";
isHide = !isHide;
};
};
```
- 6.运算符的优先级



## 循环
- continue 跳出==本次循环==（不能写到三元运算符中）
```
for(var i = 0;i<5;i++){
if(i==3){
continue;//跳出本次循环
}
console.log(i);
}
```
- break  终止==整个循环==
```
for(var i = 0;i<5;i++){
if(i==3){
break;
}
console.log(i);
}
```
- break 默认只会终止包着它的循环。
```
for(var i = 0;i<5;i++){
for(var j=0;j<5;j++){
if(i==3&&j==3){
break;
}
console.log(i,j);
}
}

//终止指定的for循环
name:for(var i = 0;i<5;i++){
for(var j=0;j<5;j++){
if(i==3&&j==3){
break name;
}
console.log(i,j);
}
}
```
## 对象
>是一种复杂类型的数据，在对象中我们可以存储任意类型的数据
- 对象存储数据，是存在对象的属性中
- ==对象是没有length这个值的==
- 属性赋值：obj.key = value;
- 属性操作：
- 第一种方式：
- 读操作：obj.属性名;
- 写操作：ojb.属性名 = 属性值;
- obj.key = value;//键值对
- 第二种方式：
- 读操作：obj["属性名"];
- 写操作：ojb[“属性值”] = 属性值;
- obj["key"] = value;//键值对

**【注意：第二种操作方法[]写的是一个字符串，如果说我们的属性名想要存在变量中，只能用[]这种方式。】**
```
var w = "width";
//注意第一种属性操作是写死的一个值，不能使用变量obj.w，这么写就认为在找obj的属性
console.log(obj.w);
//第二种属性操作，接受的是一个字符串，字符串就可以存在变量中，可以直接写obj[变量调用]
console.log(obj[w]);
```
## 循环
### in运算符
>判断这个对象中是否存在该属性，返回的是false或者是true；

```
var obj = {};
obj['name'] = "Leo";
obj['age'] = 40;
obj['gender'] = "female";
obj['width'] = "180px";
obj['height'] = "180px";
obj['children'] = ["大明","小明","三明"];

alert("name" in obj); // obj 有 name属性就返回 true，否则 返回false

for (var s in obj) { //通过 in 方法，每次循环的时候把 循环变量s 变成obj对应属性名字 
console.log(s,obj[s]);
}
```
### for in：可以用来循环 对象和数组，不能用来循环一组元素。
```
var arr = [1,4,23];
/*
for in 可以用来循环 对象和数组,不能用来循环一组元素
for 只能用来循环 数组和类数组(一组元素)
*/
for (var s in arr) { // 找到 arr上的所有属性,s会依次变成 arr的属性名
console.log(s,arr[s]);// s的类型是字符串
}
```
### for 只能用来循环 数组和类数组（一组元素）

### while循环
- 语法：
```
while(判断语句){
执行语句;
自增;
}

var i = 0;
while(i < 5){
console.log(i);
i++;
}
```

### switch:
- 语法：
```
var a = 15;
switch(a) {
case 10: // 当 a == 10
console.log("我想给大家放天假");
break; //a == 10的语句结束之后 添加break
case 15: // 当 a == 15
console.log("当然我就是想想");
break;    
case 20: // 当 a == 20
console.log("其实我真正想的是带大家出去玩");
break;
default: //以上所有的判断都不成立
console.log("还是写作业吧");
}
```
- 穿刺
- 1.case成立会把他下边所有的代码都执行了，直到遇到break
- 2.如果没写鞋break的话，就会形成穿刺现象，把下边所有的代码都执行了。
