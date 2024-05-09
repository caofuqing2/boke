---
title: javascript(十)
date: 2019-03-21 16:43:55
tags:
categories: JavaScript
---
## 练习讲解
### console.time();
> 打印执行时间

#### 注意：操作了元素的innerHTML之后，元素子元素上的所有js事件都会失效，除非写的是行间事件。

## 函数
>在实际编码中，会有很多的一些代码可能重复出现，为了能简化程序开发，重复利用，所以有了函数的概念。(function功能方法，把一个个零散的带吗和数据，组合成一个完整的方法)

定义函数
<!-- more -->

```
function fn(){
alert(1);
}
var fn2 = function(){
alert(2);
}
fn2();
/*函数调用*/
fn(); //直接调用
document.onclick = fn2;//事件调用
document.onclick();//2
document.onclick();//2
```
### 匿名函数
>函数表达式 -- 匿名函数自执行 
1. (函数)();
2. !函数();
3. ~函数();
4. +函数();
5. -函数();
```
(function(){
alert(1);
})();
!function(){
alert(2);
}();
+function(){
alert(3);
}();    
```
## 传参
>函数拥有多个参数，注意再使用的时候，行参和实参要一一对应。

- 语法：
```
function fn(a形参){
alert(a参数使用);
}
fn(实参);
```
- 实例：
```
function fn(a,b){
alert(a + b);
}
fn(1,5); //6
fn(2.3); //5
```

## 讲解剖析【选项卡】
```
//把要操作的大盒子和事件通过传参的形式传递
tab("#wrap","onmouseover");
tab("#wrap2","onclick");
function tab(id,ev) {
var wrap = document.querySelector(id);
var navs = wrap.querySelectorAll('nav a');
var cons = wrap.querySelectorAll('.cons>div');
for(var i = 0; i < navs.length; i++){
navs[i].index = i;
navs[i][ev] = function(){
for(var i = 0; i < navs.length; i++){
navs[i].className = "";
cons[i].className = "";
}
this.className = "active";
cons[this.index].className = "show";
};
}
}
```
## 讲解剖析【选中编辑】
```
<ul class="list">
<li>
<span class="info">写点啥呢</span>
<a href="javascript:;" class="editBtn">编辑</a>
<div class="edit">
<input type="text" name="">
<a href="javascript:;">确定</a>
<a href="javascript:;">取消</a>
</div>
</li>
</ul>
<script type="text/javascript">
/*
具体思路分析：
点击编辑按钮:
1) 找到edit 显示出来
2) 把info的innerHTML，添加给输入框做内容
点击取消按钮：
找到edit 隐藏
点击确定按钮:
1) 判断输入框中的内容如果为空弹出提示，否则执行下边的内容
2)     把输入框的内容添加给span的innerHTML
3)    edit 隐藏
*/    
window.onload = function() {
var li = document.querySelectorAll('.list li');
// setEdit(li[0]);
// setEdit(li[1]);
// setEdit(li[2]);
for(var i = 0; i < li.length; i++){
setEdit(li[i]);
}
function setEdit(li){
var info = li.querySelector('.info');
var editBtn = li.querySelector('.editBtn');
var edit = li.querySelector('.edit');
var text =  edit.querySelector('input');
var btns = edit.querySelectorAll('a');
editBtn.onclick = function(){
edit.style.display = "block";
text.value = info.innerHTML;
}; 
btns[0].onclick = function(){
if(text.value == "") {
alert("请输入内容");
} else {
info.innerHTML = text.value;
edit.style.display = "none";
}
};
btns[1].onclick = function(){
edit.style.display = "none";
};
}
};
</script>
```
## 讲解剖析【点击图片切换】
```
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Document</title>
<style type="text/css">
p {
margin: 0;
}
.wrap {
position: relative;
width: 300px;
margin: 30px auto;
}    
.wrap img {
display: block;
}
.wrap p {
position: absolute;
left: 0;
right: 0;
font: 14px/30px "宋体";
text-align: center;
background: rgba(255, 255, 255, .4);
}
.wrap p:first-of-type {
top: 0;
}
.wrap p:last-of-type {
bottom: 0;
}
.btn {
position: absolute;
top: 204px;
width: 40px;
height: 40px;
background: #000;
font: 14px/40px Arial;
color: #fff;
text-decoration: none;
text-align: center;
}
.btn:first-of-type {
left: -40px;
}
.btn:last-of-type {
right: -40px;
}
</style>
<script type="text/javascript">
var data = [
{
name: "童童",
img: 'img/1.JPG',
},
{
name: "学辉",
img: 'img/2.JPG',
},
{
name: "承龙",
img: 'img/3.JPG',
},
{
name: "老刘",
img: 'img/4.JPG',
},
{
name: "老王",
img: 'img/5.JPG',
}
];
window.onload = function() {
var wrap = document.querySelector('.wrap');
var img = wrap.querySelector('img');
var txt =  wrap.querySelectorAll('p');
var btns =  wrap.querySelectorAll('a');
var now = 0;
btns[0].onclick = function(){
tab(-1);
};
btns[1].onclick = function(){
tab(1);
};
function tab(dis){
now += dis;
if(now < 0 ){
now = data.length-1;
} else if(now > data.length-1){
now = 0;
}
img.src = data[now]["img"];
txt[0].innerHTML = (now + 1) + "/" + data.length;
txt[1].innerHTML = data[now]["name"];
};
};    
</script>
</head>
<body>
<div class="wrap">
<img src="img/1.JPG">    
<p>1/5</p>
<p>童童</p>
<a href="javascript:;" class="btn">prev</a>
<a href="javascript:;" class="btn">next</a>
</div>
</body>
</html>
```
## arguments
>不定参，函数所有参数的集合
- 获取其中一个参数：用下标。
- 获取参数的总个数：length。
- 参数其实就相当于函数的局部变量，只定义形参不传参的话，参数就是undefined
```
function fn(a,b,c,d) {
alert(c);//undefined
}
fn(1,2);
```
- 有一个函数，传进来的参数是不固定的，现在要计算出所有的参数和。
```
function fn() {
console.log(arguments.length);
var nub = 0 ;
for(var i = 0; i < arguments.length; i++){
nub += arguments[i];
}
alert(nub);
}
fn(1,1,1);
```

## 返回值return
>每个函数中都可以存储数据，存储的数据，可以再函数执行完成之后拿到。
- return 函数返回值（函数执行完成之后，返回的数据）
- 只能在函数中使用
- return 后面跟得值为函数执行后的返回值。
```
function a(){
return [1,2,3];
}
var b = a();
alert(b); //1,2,3
```
- 每个函数都有一个返回值，如果我们没有定义，返回值就是undefined
```
function a() {
var nub = 10;
}
var b = a();
alert(b);//undefined;
```
- 函数中 return后边的内容不会被执行(在函数执行时，会把return后边的数据返回，然后函数执行到此结束)
```
function a() {
var nub = 10;
return nub;

alert(nub*nub);
}
var b = a();
alert(b);
```
解题剖析【封装获取元素】
```
function $(){//通过id获取元素
return document.getElementById("btn");
}
window.onload = function(){
var btn = $();
console.log(btn);
}
```
## 封装
>函数：function 功能方法:把一个个零散的代码和数据，组合成一个完整的方法.

## 解题剖析【获取样式】
- getComputedStyle(box)["width"]//标准下获取计算后的样式（标准下的内置函数）
- box.currentStyle["width"]//IE下获取计算后的样式
```
function getStyle(el,attr){
if(el.currentStyle){
return el.currentStyle[attr];
}
return getComputedStyle(el)[attr];
}
var box = document.getElementById('box');
box.onclick = function(){
var left = parseFloat(getStyle(box,"left"));
box.style.legt = left + 5 + "px";
}

```

