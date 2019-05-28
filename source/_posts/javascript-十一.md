---
title: javascript(十一)
date: 2019-03-21 16:43:56
tags:
categories: JavaScript
---
## 作用域【scope】
> 一段程序代码中所用到的数据并不总是有效/可用的，而限定这个数据的可用性的代码范围就是这个名字的作用域。【一条数据可以在哪个范围中使用】

- 作用域的使用提高了程序逻辑的局部性，增强程序的可靠性，减少名字冲突
- 一个变量是全局变量，还是局部变量主要来看变量声明的位置,==声明在函数内部，就是这个函数的局部变量.==
- 在js的ECMAScript5.1中，只有函数可以产生作用域
- 当我们声明一个函数的时候，同时该函数就会创建一个属性这个属性是[[Scopes]](作用域),我们在这个函数中 声明的变量都会被存入这个函数的[[Scopes]]属性中

函数外部的变量不可以访问函数内部的局部变量数据。
<!-- more -->

```
var i = 10;
function fn(){
for(var i = 0;i<100;i++){

}
}
fn();
alert(i); //10
原因：因为for循环的时候var(声明)了i，所以i只是作为fn内部的局部变量，alert(i)在外面是不能获取到的。
```
第二个var预解析,但是只会把预解析提到当前script(或function)的最前面。
```
<script>
var i = 0;
</script>
<script>
alert(i); //0
</script>
__________________
<script>
alert(i);
</script>
<script>
var i = 0;
</script>
```
### 全局作用域（全局变量）【在任何地方都能访问】
>没有声明在任何函数内部的变量，就是全局，全局变量在全局的任何地方就可以调用和修改，尽量不要使用全局变量，会造成全局污染
- ==函数外定义的变量==拥有全局作用域
- ==不使用var定义的变量==拥有全局作用域
- ==所有window对象上的属性==拥有全局作用域
- ==没有声明在任何函数内部==的函数拥有全局作用域
```
1.加在window上边的内容作用域属于全局的，
属于window的属性，可以不用写window，直接写属性名就行
function fn(){
window.nub = 100;
}    
fn();
alert(nub);



2.变量如果不加声明，就默认认为是window的内容，作用域变成全局了
function fn(){
nub = 100;
}    
fn();
alert(nub);

3.没有声明在任何函数内部的变量(全局),就是全局变量。
在全局的任何地方就可以调用和修改,尽量不要使用全局变量，会造成全局污染
var nub = 0;
function fn(){
nub = 10;
}
fn();
alert(nub);

```
#### 全局命名空间污染：
>在程序中经常需要引用一些库，如C++编译系统提供的标准库、由第三方软件开发商提供的开发库或者用户自己开发的库等。如果在这些库中含有与程序中定义的全局实体同名的实体，或者不同的库之间有同名的实体，则在编译时都会出现名字冲突，这就称为全局命名空间污染 (命名冲突)

### 局部作用域（局部变量）【只能在函数内部访问】
- 使用var在函数内部定义的变量,和使用function在函数内部声明的函数,拥有局部作用域
```
//i在当前的函数中定义为0，下面的函数中并没有这个i，所以报错
(function(){
var i = 0;
})();
(function(){
alert(i); //报错
})();
```
## 作用域链
>当我们调用一个变量或者函数的时候，首先会在当前作用域下找该变量和函数的声明，如果当前作用域下没有，则会找当前作用域上一级作用域，直到找到或找到全局作用域下是否有声明，如果还有没有，则报错。

### 变量与函数的查找规则：
- 当我们调用一条数据的时候，js首先会在当前作用域中进行查找，如果找不到，就向上找到父级的作用域，如果在父级的作用域中也找不到，就继续向上查找，直到window的作用域。如果在window中也找不到，就报错了。如果在当前作用域中找到了，那就用当前的。

## 预解析
>浏览器每读到一个script标签或function，先不执行任何代码，会先把整个代码快速的浏览一遍，然后从中 挑出 var 和 function两个关键字 .
- var： 预解析遇到 var 就把 ==var 连同它后边的名字==一块 提到script(或function) 的最前边,预解析完成之后，在从上向下一行一行执行代码，如果碰到了 = 就赋值;
- function:预解析遇到function,就把整个函数提到提到==script(或function) 的最前边==（跟在var的后边预解析先解析var 再解析 function）
```
alert(b);//function b(){console.log(1);}
function b(){
console.log(1);
}
var b = 0;
解析步骤：
var b;
function b(){
console.log(1);
}
alert(b);
```
```
<script type="text/javascript">
alert(b); // function b(){ var b = 10; }
var b = 0;
alert(b); // 0
function b(){ var b = 10; }    
alert(b); // 0   
var b = 20;
alert(b); //20
var b = function(){ var b = 30;}
alert(b); // function(){ var b = 30;}

解析步骤：
var b;
var b;
var b;
function b(){var b = 10;}
alert(b);
var b = 0;
alert(b);
alert(b);
var b = 20;
alert(b);
var b = function(){var b = 30;}
alert(b);
</script>
```

```
<script type="text/javascript">
alert(a);
</script>
<script type="text/javascript">
var a = 100;
</script>
```
## 闭包
>函数嵌套函数产生一个闭包环境，内部函数可以访问外部函数的局部变量数据,但是外部函数不能访问内部函数的局部变量数据。

```
function fn(x) {
return function(y){
alert(x + y);
};
}    
var bar = fn(2);
bar(10);

//解析
var bar;
function fn(x){
return function(y){
alert(x+y);
};
}
var bar = fn(2);
var bar = function(y){
alert(2+y);
}
bar(10);
function bar(10){
alert(2+10); //12;
}
```
## 闭包应用
```
var btn = document.querySelectorAll('input');
function setEv(nub){
btn[nub].onclick = function(){
alert(nub);
}
}
/*setEv(0);
setEv(1);
setEv(2);*/
for(var i = 0; i < btn.length; i++){
setEv(i);
}
_________________________
var btn = document.querySelectorAll('input');
for(var i = 0; i < btn.length; i++){
//每一次都自执行一次，然后把每次循环的i值通过形参传入
(function(index){
btn[index].onclick = function(){
alert(index);
}
})(i);
}

——————————————————————————
var btn = document.querySelector('input');
function setEv(){
var nub = 0;
return function(){
nub++;
alert(nub);
};
}
// var fn  = setEv();
// fn();
// fn();
btn.onclick = setEv();

解析：
var nub = 0;
btn.onclick = function(){
nub++;
alert(nub); //1 2 3 ....
}
```
## 内存泄漏
问题：当内部函数被外部所引用的时候，那么闭包函数所产生的数据将不会被垃圾回收，可能会造成程序中的数据在内存所占用的空间得不到及时的释放，从而产生内存泄漏。
