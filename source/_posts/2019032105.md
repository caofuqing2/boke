---
title: javascript(七)
date: 2019-03-21 16:43:52
tags:
categories: JavaScript
---
## 第一章复习
### 1.获取元素的方法
- 获取单个元素：
- document.getElementById('idName');//只能从document获取
- document.querySelector('cssSelector');//可以从父级获取
- 获取一组元素//都可以从父级获取
- document.querySelectorAll('cssSelector');
- document.getElementsByTagName('tagName');
- document.getElementsByClassName('className');
- query和get方法的区别：
- query方法只会在声明的时候，获取一次。
- get方法每次使用的时候，都会获取一次。
<!-- more -->

### 2.事件
- onload：加载完成之后（只有window、body能加onload事件）
- onclick：点击事件
- onmonuseover 鼠标移入
- onmouseout 鼠标移除

### 3.变量
- 用来存储数据的一种方式（存值、存址）。
- 变量声明：var 变量名 = 要存储的具体数据
- 规则：在那个函数中声明的变量，就职能在这个函数中使用。

### 4.变量命名
1. 可以使用字母、数字、$、_。
2. 变量名不能以数字开头
3. 驼峰命名：从第二个单词开始首字母大写
4. 常量命名：字母全部大些，每个单词中间用“_”隔开
5. 注意关键字和保留字不能用于变量名

### 5.函数
- 匿名函数：没有名字的函数function(){};
- 有名字的函数：
函数声明：function name(){ //执行语句 }
- 函数调用：
- 事件调用：
- el.onclick = name;
- el.onclick = function(){}
- 直接调用
- name();

### 6.属性操作
- 属性的读操作
- 属性读操作(获取属性值):obj.属性名
- 属性写操作(获取修改属性值):obj.属性名 = 属性值；
- 注意问题：
- 1.clsss不叫class，叫className
```
document.getElementById('div').className;
```
- 2.style 操作的是元素的行间样式
```
<div id="div" style="border:#f00 1px solid;"><div>
<script>
document.getElementById('div').style;
</script>
```
- 3.获取src的时候获取到的是绝对路径
- 4.获取background这类符合样式的时候，火狐（firefox）下可以获取到符合样式中的所有样式而谷歌（chrom）下获取到的只是我们写了的样式
- eg:只设置了一个background:color。
```
<div id="div" style="background:blue"></div>
<script>
/*
*火狐得到的是:blue none repeat scroll 0% 0%;
*谷歌得到的是：blue
*/
document.getElementById('div').style.background;
</script>

```
- 5.设置了十六进制颜色，但是获取的时候，获取到的是rgb颜色
- eg:background:#f60,得到的是rgb(255, 102, 0)
```
<div id="div" style="background:#f60"></div>
<script>
/*
* 得到的是rgb(255, 102, 0) 
*/
document.getElementById('div').style.background;
</script>

```
- 6.遇到“-”，删除“-”，首字母大写
- eg:background-color  => backgroundColor
```
<div id="div" style="background:#f60"></div>
<script>
document.getElementById('div').style.backgroundColor;
</script>

```
- 7.把等号右侧的值赋给左侧
```
var sum = 100;
```
- 8.cssText获取**style**中所有的内容
- 直接修改cssText会覆盖style中的所有内容，如果不想覆盖之前的所有内容，可以直接写style，或者用+=；
```
<div id="div" style="background:#f60;"></div>
<script>
var div = document.getElementById('div');
//这个时候style="color:#f00;"
div.cssText = "color:#f00;"
//这个时候style="background:#f60;color:#f00;"
div.cssText +="color:#f00;"
</script>

```
- 9.cssText = "" 可以直接清空所有的行间样式。
```
<div id="div" style="background:#f60;"></div>
<script>
var div = document.getElementById('div');
//这个时候style被清空
div.cssText = ""
</script>
```

- 10.innerHTML 代表元素中的所有内容
- 从元素的开标签到闭合标签之间的所有内容，包括元素中的子元素
- 直接设置元素的innerHTML,或者替换掉之前的所有内容，如果不想替换只是添加内容用+=； 
```
<div id="div"><span>aa</span></div>
<script>
var div = document.getElementById('div');

//<div id="div">aaa</div>
div.innerHTML = "aaa"

//<div id="div"><span>aa</span>aaa</div>
div.innerHTML += "aaa"
</script>
```
- 11.在写left，width等样式时，一定注意加单位
- 可以给元素设置它本身不具备的属性，这个叫自定义属性。
- 自定义属性：
- 1.对象本身不具备的属性（不是标准中规定的属性，而是我们自己设置的）
- 2.索引中：在实践中，需要知道当前元素是一组元素中第几个的时候，需要使用索引值。

### if语句
- 扩展：
- 字符串：引号包起来的一串自负
- 布尔值：true 和 false
- 运算符：
- 1.“+”：
1. 如果加号左右两边是数字，执行加法运算。
2. 如果一遍是字符串，执行字符串链接。

- 2.执行数字运算：“*,/,-,%,--,-=,++,+=”
- 3.逻辑运算符，返回的结果是布尔值：>,==,<,>=,<=,!=;
- 4.!非（否） 布尔值中取反
- 语法:
> 同一个位置，需要两种或两种以上的执行结果，用判断。

```
if(布尔值){

}

if(布尔值) {//布尔值为true执行if，为false接着向下执行

}else if(布尔值) {

}

if(布尔值) {

} else if(布尔值) {

} else {

}
```

### for循环：
>当我们需要同时操作一组元素，或者一组数据的时候需要用到循环。
1. 初始值：var i = 0;
2. 判断条件：i < li.length;
3. 执行语句：执行里面面的操作;
4. 自增：i++;

执行顺序：1，2，3，4

for(初始值;判断条件;自增){
//执行语句
}

### 数组：
- 用来存储一组数据
- 格式[data1,data2,data3]
- 每一个数据之间用，隔开
- 一组数据不能直接操作，要操作一位需要使用下标。
- 需要使用下标
- 可以从数组length获取到数组中存储多少位数据。


### this：
1. 事件函数中
2. this指向，触发当前事件的元素
3. 目前的非事件函数，this指向window


### 思路：
1. 定点清除
- 1.先清楚选中的元素的样式。
- 2.给当前的元素加上选中样式。
- 3.定义个变量记录之前选中的元素和当前选中的元素。
2. 自定义属性
3. 大清洗
- 1.先清除所有元素的选中样式
- 2.给当前的加上选中样式
