---
title: javascript(六)
date: 2019-03-21 16:43:51
tags:
categories: JavaScript
---
## 获取方式区分：
1. query相关的方法，再使用时就只获取一次。
2. get方法在每次我们调用的时候，都会重新获取一次。

## onclick清空
box.onclick = null//把box的onclick事件变成空对象。

## 索引

- 定义一个元素本来不存在的属性，自定义属性。
<!-- more -->

```
for(var i = 0;i<lis.length;i++){
//自定义属性可以是中文，可以是英文，可以是数字，但是尽量的要使用小写英文字母。
lis[i].序号 = i;

}
```
- 特定的属性index（索引）。
```
for(var i = 0;i<lis.length;i++){
lis[i].index = i;
lis[i].onclick = function(){
alert(this.index);
}
}
```
