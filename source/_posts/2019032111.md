---
title: javascript(一)
date: 2019-03-21 16:43:46
tags:
categories: JavaScript
---
## javascript(JS)的组成？
- DOM 文档对象模型
- BOM 浏览器对象模型（滚动条之类） [没有标准，也就意味着兼容性不好]
- ECMAScript 核心(翻译器)

## javascript(JS)在页面中处理了什么事情？
- 特效交互
- 数据交互
- 逻辑操作
<!-- more -->

## 常见特效的原理
- 通过js修改元素的css样式，来操作元素的变化。

## js可以写在那里？
注意：行为(js)，样式（css），结构（html）三者分离
- 写在标签内部，行间事件【不建议这样写，不容易实现分离】
- 在标签上通过一些特殊属性，比如onclick，onmouseover等来实现行为的，并且这个行为和当前元素进行了绑定。
```
<!--行内js 作用于标签上面-->
<button onclick="alert(123)">按钮</button>
```
- 写在页面内部专门的script标签中，当浏览器读到script的时候就会解析代码。
```
<button id="but2">按钮2</botton>
<script>
document.getElementById("but2").onclick = function(){
alert('就是这么绑定事件！');
}
</script>
```
- 写在外部调用，专门的js文件中【通过src引入】
```
<!--外链JS-->
<script src="js/1.js"></script>
```

## 获取元素
- 如果要获取的是个id，可以直接写元素的id名[存在浏览器兼容问题]
- document.getElementById("idName"); 获取Id

- 【单、双引号都可以，但是要成对存在】
- 【翻译：在文档中 获取 元素 通过 ID】
- 【获取该元素之前，请确保元素已经被解析了】

```
<script>
document.getElementById("but").onclick = function(){
document.getElementById("div1").style.width  = "200px";
document.getElementById("div1").style.height = "200px";
}
</script>
```

## 属性操作
- 属性的读操作(获取元素的属性值)
- clsss不叫class，叫className
```
document.getElementById('div').className;
```
- style 操作的是元素的行间样式
```
<div id="div" style="border:#f00 1px solid;"><div>
<script>
document.getElementById('div').style;
</script>
```
- 获取src的时候获取到的是绝对路径
- 获取background这类符合样式的时候，火狐（firefox）下可以获取到符合样式中的所有样式而谷歌（chrom）下获取到的只是我们写了的样式
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
- 设置了十六进制颜色，但是获取的时候，获取到的是rgb颜色
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
- 遇到“-”，删除“-”，首字母大写
- eg:background-color  => backgroundColor
```
<div id="div" style="background:#f60"></div>
<script>
document.getElementById('div').style.backgroundColor;
</script>

```

- 属性的写操作(修改元素的属性值)

**【注意： 在写left，width等样式时，一定注意加单位 】**
- 把等号右侧的值赋给左侧
```
var sum = 100;
```
- cssText获取**style**中所有的内容
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
- cssText = "" 可以直接清空所有的行间样式。
```
<div id="div" style="background:#f60;"></div>
<script>
var div = document.getElementById('div');
//这个时候style被清空
div.cssText = ""
</script>
```

- innerHTML 代表元素中的所有内容
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



## 字符串
- 一种数据格式，引号包起来的一串字符

## undefined
- 一种数据类型，未定义

## +号运算符
- 加法运算
- 链接两个字符串
- +=（a += b  --- a = a + b）
- 加号有两个作用
- 一个是加法运算
- 一个是字符串链接：只有加号左右两侧是数字的情况才会执行加法运算，如果有一侧是字符串就会执行字符串链接，结果也是字符串。

```
var a = "哈哈哈";
var b = 1000;
console.log(a+b);//哈哈哈1000
console.log(b+a);//1000哈哈哈
```

## 变量
- 变量就相当于给数据起了一个简短的名字
- 变量的作用：为了方便数据的复用和维护，我们通常用一个东西存放这类数据，我们就把它称为变量。
- 变量声明
- var 变量名 = 要存储的具体数据
- 变量命名：
- 1. 以字母开始
- 2. 变量在命名时最好带有含义
- 3. 注意不能使用关键字和保留字
- 4. 驼峰方式命名
- 5. 不能以数字、特殊符号（除了$,_）开头
- 6. 后续内容不能包含特殊符号（除了$,_）
```
<button id="but">按钮1</button>
<div id="div1"></div>
<script>
var but1 = document.getElementById('but');
var div1 = document.getElementById('div1');
btn1.onclick = function(){
div1.style.width = "200px";
div1.style.height = "200px";
div1.innerHTML = "您好！"；
}
</scirpt>
```

## 函数
- 有名字的函数
函数声明：
function name(){
要执行的内容
}
调用:name();

- 匿名函数【不能直接使用，只能使用在事件中】
- eg:btn1.onclick = function{要执行的内容}
- 函数调用：把函数执行一遍
- 事件调用 btn.onclick = name;[注意不加括号]
- 非事件调用：添加括号

【*注意：btn.onclick = name(); 只会直接执行一次，当点击btn的时候就不执行了；】

【*注意：btn.onclick = function(){name()}; 不直接执行，当点击btn的时候执行；】

- 什么时候加括号，什么时候不加括号？
- 1.当浏览器直接读到这行代码的时候，就执行需要给函数调用加（）；
- 2.当某种特定的条件下才执行，不需要加（）；

## window和window.onload
- onload事件 加载完成

## onmouseover和onmouseout
> 鼠标移入和移出

## 调试工具：
- alert()【弹出对话框，接受的是一个字符串】
- console.log【打印控制台】

* 控制台
* F12，或者右键->审查元素方式可以打开调试工具
* 选择：console
* 可以通过console进行数据输出，分析，代码调试

```
<button id="btn">按钮1</button>
<div id="div1"></div>
<script>
var div1 = document.getElementById('div1');
var div1 = document.getElementById('div1');
btn1.onclick = function(){
//把信息以日志方式打印到控制台中
console.log("你好");
//打印数据信息结构
console.dir(div1);
}
</script>
```
