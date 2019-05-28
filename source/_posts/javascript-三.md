---
title: javascript(三)
date: 2019-03-21 16:43:48
tags:
categories: JavaScript
---
## 数组
- 数组[] Array是一种数据格式。
- 数组中，每个数据之间用“,”隔开。
- 获取数组中的其中一位，需要用下标。
- 数组的长度 length。
- 数组中可以存放任意类型的数据,但是一般为了代码的可读性极维护性，我每一个数组中，只存放一种类型的数据。
- 当判断不大于这个数组的时候可以两种方式。
- i>=arr.length-1;
- i>arr.length
<!-- more -->

```
var = [123,"abc",true,document,function(){},,"",[]];
console.log(arr[5]); //undefined;
console.log(arr.length);//8

```
## 练习和作业
**详细分析：**
1. 布局
2. 获取元素，定义变量，定义数组
2. 循环切换和顺序切换的按钮
- 1.点击切换下面的文字说明。
- 2.点击加className,去掉另一个的className
3. 循环切换
- 1.点击左边箭头控制数字一直减，到0的时候回到5.
- 2.点击右边尖头控制数字一直加，到最大的时候回到0.
- 3.上面的1/4修改值
- 4.切换文字描述
4.顺序切换
- 1.点击左边箭头控制数字一直减，到0的时候弹出提示，并且下面的不能点击.
- 2.点击右边尖头控制数字一直加，到最大的时候弹出提示，并且下面的不能点击.
- 3.上面的1/4修改值
- 4.切换文字描述
```
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Title</title>
<style>
body{
font-family: Arial;
}
p{
margin: 20px 0;
padding:0;
}
input{
outline: none;
}
.wrap{
position: relative;
width:550px;
margin:50px auto 0;
}
.tab{
width:550px;
margin:0 auto;
text-align: center;
background-color: #000;
padding:20px 0;
}
.tab div{
width:164px;
margin:0 auto;
}
.tab div::after{
content:".";
display:block;
height:0;
clear:both;
}
.tab input{
display: inline-block;
border-radius: 3px;
width: 80px;
line-height:20px;
margin-left:-1px;
border:#fff 1px solid;
background: #000;
color:#fff;
float: left;
cursor: pointer;
}
.tab input.cur{
background: #fff;
color:#000;
}
.tab p{
color:#ccc;
font-size: 13px;
}
.box{
margin: 0 auto;
width: 550px;
height: 310px;
position: relative;
}
.box input{
position: absolute;
top: 50%;
margin-top:-25px;
width: 40px;
height: 50px;
border: 0;
background: none;
color:#fff;
font-size: 26px;
}
.box input:hover{
background-color: rgba(0,0,0,.4);
cursor: pointer;
}
.box input:nth-of-type(1){
left: 0;
}
.box input:nth-of-type(2){
right:0;
}
.box nav{
position: absolute;
left:0;
bottom:0;
width:100%;
line-height:40px;
color: #fff;
text-align: center;
background-color: rgba(0,0,0,.3);
}
.box span{
position: absolute;
width:100%;
line-height:45px;
text-align: center;
top:0;
color: #fff;
}
.mask{
position: absolute;
display: none;
top:0;
left:0;
width:100%;
height:100%;
background-color: rgba(255,255,255,0);
z-index: 99;
}
.fixed{
width: 300px;
height:150px;
position: absolute;
left:50%;
margin-left: -150px;
top:50%;
margin-top: -75px;
background-color:rgba(0,0,0,.8);
color:#fff;
text-align: center;
}
.fixed p:nth-of-type(2){
font-size: 12px;
}
.fixed a{
text-decoration: none;
color:#fff;
font-size: 12px;
}
.fixed a:nth-of-type(1){
border:#fff 1px solid;
padding:5px 15px;
}
.fixed a:nth-of-type(2){
position: absolute;
right:10px;
top:10px;

}
</style>
</head>
<body>
<div class="wrap">
<div class="tab">
<div>
<input type="button" value="循环切换" class="cur">
<input type="button" value="顺序切换">
</div>
<p>图片可以从最后一张转到第一张循环</p>
</div>
<div class="box">
<span>1/4</span>
<input type="button" value="<">
<img src="img/1.jpg" />
<input type="button" value=">">
<nav>文字描述一</nav>
</div>
<div class="mask">
<div class="fixed">
<p>Javascript 提醒</p>
<p>已经到第一张啦～</p>
<a href="javascript:">确定</a>
<a href="javascript:">X</a>
</div>
</div>
</div>
<script>

//获取控制循环和顺序的元素
var tab = document.querySelector('.tab');
var tabP = tab.querySelector('p');
var tabs = tab.querySelectorAll('input');

//获取要进行修改处理的元素
var box = document.querySelector('.box');
var inputs = box.querySelectorAll('input');
var span = box.querySelector('span');
var img = box.querySelector('img');
var navText = box.querySelector('nav');

//弹出提示框
var mask  = document.querySelector('.mask');
var fixed = document.querySelector('.fixed');
var fText = fixed.querySelectorAll('p')[1];
var fSure = fixed.querySelectorAll('a');

//创建数组
var arrImg = ['img/1.jpg','img/2.jpg','img/3.jpg','img/4.jpg'];
var arrImgText = ['文字描述一','文字描述二','文字描述三','文字描述四'];
var arrText = ['图片可以从最后一张转到第一张循环','图片只能到第一张或者最后一张'];

var srcNum = 0,max = arrImg.length-1,min = 0,isIn = true;

tabs[0].onclick = function() {
isIn = true;
toFunText();
}
tabs[1].onclick = function() {
isIn = false;
toFunText();
}

//切换按钮的样式和文字变换
function toFunText(){
if(isIn){
tabP.innerHTML = arrText[0];
tabs[0].className = 'cur';
tabs[1].className = '';
}else{
tabP.innerHTML = arrText[1];
tabs[1].className = 'cur';
tabs[0].className = '';
}
}
//上一张
inputs[0].onclick = function(){
srcNum-- ;
if(srcNum<min){
if(isIn){
srcNum = max;//循环
}else{
srcNum = min;
//alert('这是第一张');
fText.innerHTML = '已经是第一张了哦～';
mask.style.display = 'block';
}

}
img.src = arrImg[srcNum];
navText.innerHTML = arrImgText[srcNum];
span.innerHTML =(srcNum+1)+'/'+arrImg.length;

}
//下一张
inputs[1].onclick = function(){
srcNum++ ;
if(srcNum>max){
if(isIn){
srcNum = min;//循环
}else{
srcNum = max;
fText.innerHTML = '已经是最后一张了哦～';
mask.style.display = 'block';
//alert('这是最后一张')
}

}
img.src = arrImg[srcNum];
navText.innerHTML = arrImgText[srcNum];
span.innerHTML =(srcNum+1)+'/'+arrImg.length;

}
//点击关闭提示弹框
fSure[0].onclick=function(){
closeFun();
}
fSure[1].onclick=function(){
closeFun();
}
function closeFun(){
mask.style.display = 'none';
}
</script>
</body>
</html>
```
