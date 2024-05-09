---
title: javascript(八)
date: 2019-03-21 16:43:53
tags:
categories: JavaScript
---
## ECMAScript
## 数据类型划分
#### 1、标准指定的类型划分：
- 基本类型：
- 1.number（数字）
- 2.string（字符串）
- 3.undefined（未定义）
- 4.boolean（布尔值）
- 5.null（空对象）找不到对象，对象未定义。与非空对象最大区别在于是否能进行属性操作。
<!-- more -->

- 对象类型（复合类型）：object(对象)，包含Array;
#### 2、typeof的方式划分
>typeof是一种运算符，用来查看类型。
- 1.number:【从负无穷到正无穷的数字及NaN=》not a Number】
- Number.POSITIVE_INFINITY 正无穷
- Number.NEGATIVE_INFINITY 负无穷
- 2.string:【字符串，任何包含在引号中的一串字符，都属于字符串】
- 3.boolean:【true或false两种值，布尔值】
- 4.object:数组、null、元素对象(Element)、object【注意：空数组不等同于空对象，因为空数组可以进行操作，空对象不能进行属性操作】
```
console.log(null == arr);
```
- 5.function:函数类型
- 6.undefined：未定义。
- 7.NaN：非数字 not a number [类型是number]
- 1.NaN不等于任何东西，并且不等于它自己。
- 2.检测一个内容是否是NaN的时候，可以使用isNaN();
- 3.数据类型：number;
- 4.NaN不能用来做比较。
- 5.isNaN(要检测的内容) return:true/false,isNaN 隐式调用的是Number。
- 如果转化结果是一个数字就返回false
- 如果不是一个数字就返回true
- isNaN会进行隐式类型转换，转换所调用的方法是Number
```
var a = Number("10px");//NaN
var b = Number("10px");//NaN
//alert(a == b);// false
alert(isNaN("$30.2"))//true;
```


## 调试：
- console.log();//只是打印出一个元素或值等。
- console.dir();//打印对象。


## 数据类型的转换。
- 强制类型转换，或者显示类型转换。
- 字符串转换数字（强制）：
- 1.parseInt:取整 (要转换的数字,传进来的数字的进制值)
>从左向右一位一位去查看，如果遇到一位是非数字的，结束执行，把这位之前的数字返回

- 2.parseFloat：转换成小数 (转换为浮点数)
>从左向右一位一位的匹配，直到遇到一个非数字（可以匹配一个小数点）就返回这位前边的数字

- 3.Number(要转换的数字)
>从左向右看完所有的字符，如果完全符合数字的规则就转换，如果不符合数字的规则就返回NaN

- 【注意：关于数组：】
- 1.空数组转为0；（Number转的方式）
- 2.数组只有一位的时候，会用这位(代表他本身)去转换，并且只转换数字和字符串为数字的，其他的都是NaN
- 3.数组有多位的时候，只会被转换为NaN

```
var num = false;//true = 1;false = 0;
var nub;//NaN（undefined）;
var nub = null //0;
var nub = document; //NaN;
var nub = [];//0;
var nub = [0];//0;
var nub = [10];//10
var nub = [10,2];//NaN
var nub = ['aaa'] //NaN
var nub = ['10']//10
var nub = function(){}//NaN
var nub = undefined;//NaN
nub = Number(nub);
```
- 强制转成字符串
- toString();【要转换的内容.toString】
```
var a = 123;
a = a.toString(); //将数字123专为字符串类型
console.log(a,typeof a);123 string;
var b = ['','2'];
b = b.toString();
console.log(b,typeof b);//,2 string
```
- String(要转换的内容)
- 强制转成布尔值
Boolean（要转换的内容）
- 真：true,非空字符串，非0数字，非空对象。
- 假：false，空字符串，0，NaN，null，undefined
```
!取反
alert(!"21323");//false
alert(Boolean(123));//true    
```

```
var a;
if(a){
alert("真");
} else {
alert("假");
}
```


- 隐式类型转换
>浏览器自己进行转换，其他类型转换成数字，主要调取Number

- "+、+="：
- 1.当加号左右两侧有一位是字符串时，会把另外一侧也转成字符串
- 2.使用+号时，两边没有字符串时，优先尝试把左右两侧都转成数字，如果不能转换成数字就转换成字符串进行链接。
- "-"、"*"、"/"、"%"、"-="、"*="、"/="、"%="：运算符左右两侧转换成数字进行运算：

```
console.log(null + false,0 + function(){});//0 "0function(){}"
var nub = "20px";//NaN
var nub2 = "30px";//NaN
console.log(nub/nub2);//NaN
```



## 运算符
- 关系运算符： || 、 && 、！
- ||：当第一个条件返回true，就结束运行，返回true，如果第一个条件返回false，那再来看第二个条件，如果第二个条件返回true，整体也为true，如果两个条件都为false，则返回false。

- &&：当第一个条件返回false，就结束运算，直接返回false。如果第一个条件返回true，那再来看第二个条件，如果第二个条件返回false，整体也返回false，如果两个条件都返回true则返回true；

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


## 讲解剖析 【找出数组中最大的值】
```
var arr = [123,1,324,1233,20,-32,100];//定义一个数组
var max = 0;//给一个最初比较的值
/*
在这里，max可以设置成负无穷,以下是常量。
Number.POSITIVE_INFINITY 正无穷
Number.NEGATIVE_INFINITY 负无穷
*/
//循环数组
for(var i = 0; i < arr.length; i++){
//如果max小于arr[i],说明arr[i]比max大，所以把它的值赋给max。
if(max < arr[i]){
max = arr[i];
}
//返回最大的【也可直接用这种方式】
//max = Math.max(max,arr[i]);
}
alert(max);
```

## 讲解剖析【取模】
```
var list = document.querySelector('.list');
var colors = ["red","yellow","blue","green","pink"];
var inner = "";
// red blue yellow
for(var i = 0; i < 20; i++){
/*第一种方式，比较笨*/
/*if(i%3 == 0){
inner += '<li style="background:red">'+i+'</li>';
} else if(i%3 == 1) {
inner += '<li style="background:blue">'+i+'</li>';
} else if(i%3 == 2) {
inner += '<li style="background:yellow">'+i+'</li>';
}*/
/*第二种方式，不会有颜色多少的限制，可扩展性比较好，代码量少*/
inner += '<li style="background:'+colors[i%colors.length]+'">'+i+'</li>';
}
list.innerHTML = inner;
```

## 讲解剖析【复选框】
- 复选框样式控制选中用==checked==。
- 改变事件用==onchange==;
```
var input = document.querySelectorAll('input');
for(var i = 0; i < input.length; i++){
input[i].onchange = function(){
console.log(this.checked);
};
}
```
