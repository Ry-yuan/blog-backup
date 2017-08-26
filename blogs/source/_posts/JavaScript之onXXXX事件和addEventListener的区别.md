---
title: Js之on事件和addEventListener的区别
date: 2017-05-16 22:46:04
tags: JavaScript
---
### 1.首先两者的用法：
#### onXXXX的用法：以onclick为例
第一种：
```javascript
obj.onclick = function(){
//do something..
}
```

第二种：
```javascript
obj.onclick= fn;
function fn (){
//do something...
}
```

第三种：当函数fn有参数的情况下使用匿名函数来传参：
```javascript
obj.onclick = function(){fn(param)};
function fn(param){
//do something..
}
```
不能够这样写:
```javascript
obj.onclick= fn(param);
```
因为这样写函数会立即执行，不会等待点击触发

#### addEventListener的用法：
addEventListener(event,funtionName,useCapture)
参数：
event:事件的类型如 “click”
funtionName：方法名
useCapture(可选)：布尔值，指定事件是否在捕获或冒泡阶段执行。
  ● true - 事件句柄在捕获阶段执行
  ● false- false- 默认。事件句柄在冒泡阶段执行
一种：
```javascript
obj.addEventListener("click",function(){
//do something
});
```

二种，没参数直接写函数名
```javascript
obj.addEventListener("click",fn,fasle));
function fn(){
//do something..
}
```

三种：函数有参数时需要使用 *匿名函数*来传递参数
```javascript
obj.addEventListener("click",function(){fn()parm},false);
```


### 2.两者的区别
#### 2.1 on事件会被后面的on事件覆盖
以onclick为例：
```javascript
obj.onclick(function(){
alert("hello world");
});
obj.onclick(function(){
alert("hello world too");
});
```
最终会只有弹框输出：
hello world too

#### 2.2addEventListener 则不会覆盖。
```javascript
obj.addEventListener("click",function(){
alert("hello world");
}));
obj.addEventListener("click",function(){
alert("hello world too");
}));
```
这样会有：
hello world 
hello world too


### 3.addEventListener注意事项：
#### 特别说明addEventListener 不被IE9以下兼容，IE9以下用使用 attachEvent()；
形式：obj.attachEvent(event,funtionName);
event:事件类型（需要写成“onclick”前面加on，这个与addEventListener不同）
funtionName:方法名（要参数是也是需要使用匿名函数来传参）


### 4.最后奉上事件集合：
1.鼠标事件：
  ● click(单击)
  ● dbclick(双击)
  ● mousedown(鼠标按下)
  ● mouseout(鼠标移走) 
  ● mouseover(鼠标移入)
  ● mouseup(鼠标弹起)
  ● mousemove(鼠标移动)
2.键盘事件：
  ● keydown(键按下)
  ● keypress(按键)
  ● keyup(键起来)
3.HTML事件：
  ● load（加载页面） 
  ● unload（卸载）
  ● change（改变）
  ● scroll（滚动）   
  ● focus（获得焦点）
  ● blur（失去焦点）

### 5.总结：
on与addEventListener都是为dom元素添加事件监听，使其在事件发生后执行相应的代码，操作。有了它们我们实现了页面与用户交互。

作者：Ry-yuan（瑞元）
