---
title: 前端性能优化--图片懒加载(lazyload image)
date: 2017-07-25 21:37:17
tags: 前端性能优化
---
## 话说前头：
>上次写了一篇webpack的学习心得，webpack能做到提升前端的性能，其模块打包最终生成一个或少量的文件能够减少对服务端的请求。除此之外，图片懒加载也是一种优化前端性能的方式。使用懒加载可以想要看图片时才加载图片，而不是一次性加载所有的图片，从而在一定程度从减少服务端的请求。

## 懒加载介绍：
* 通俗介绍：懒加载怎么个懒法，就是你不想看就不给你看，我也懒得加载出来，懒得去请求。通俗的说就是你不要就不给你，反正你又不是我爱的人。举个栗子，比如在进入某个页面的时候，它会有许多的图片，有些图片可能在下面，当我们点进页面但没有滑动下去或没看完整个页面，那么下面的图片就会没用，加载了也白加载，而且还降低了网页的加载速度。因此懒加载就是当滚动到可视区域时才加载当前的图片。  

* 原理：图片的加载是由src的值引起，当对src赋值时浏览器就会向服务器请求图片资源，基于这个，可以利用html5新属性data-XXX来保存图片的路径，当我们需要加载图片的时候才将data-xxx的值赋予src，酱就能实现图片的按需加载，也就是懒加载了。

* 优点：提高前端性能，图片在需要的时候才加载，减轻服务的负担，提高页面的加载速度，能够减少带宽。

## 懒加载实现方式:
##### 1.使用jquery-lazyload.js，jQuery的插件用于懒加载使用，需要依赖jQuery。   
[jquery-lazyload.js演示](http://ry-yuan.me/lazyload-demo/jq-lazyload.html)
##### 2.使用echo.js：专门用于实现懒加载。
[echo.js演示](http://ry-yuan.me/lazyload-demo/echo.html)

#### -- jquery-lazyload.js 实现方式：
1.引入：在HTML中引入jQuery和jQuery-lazyload，如：
```Javascript
<script type="text/javascript" src="js/jquery-3.2.1.min.js"></script>
<script type="text/javascript" src="js/jquery.lazyload.min.js"></script>
```
2.图片中不使用src属性，因为使用src属性后就会默认发送请求请求图片，使用data-original代替，还有图片要给高度： 
```html
<img class="lazy" data-original="images/p1.jpg" style="margin-top:500px" height="300">
```
3.添加jQuery代码：
```html
<script type="text/javascript">
    $(function() {
        $("img.lazy").lazyload();
    })
</script>
```

#### -- jquery-lazyload.js的参数:
** 1.threshold **:设置Threshold参数来实现滚到距离其xx px时就加载。如：  
```javascript
$(function() {
     $("img.lazy").lazyload({
        threshold :100
    });
})

```


** 2.placeholder **:为某一图片路径.此图片用来占据将要加载的图片的位置,待图片加载时,占位图则会隐藏,比如放一些等待加载的图片来优化用户体验效果。
```javascript
$(function() {
     $("img.lazy").lazyload({
        placeholder: "images/loading.gif"
    });
})

```
** 3.event **：触发定义的事件时，图片才开始加载（此处click代表点击图片才开始加载，还有mouseover，sporty,foobar(…)）
```javascript
   $(function(){
        $("img.lazy").lazyload({
            event : "click"
        });
    })
```

** 4.effects **：图片显示时的效果，默认是show。
```javascript
     $(function(){
        $("img.lazy").lazyload({
            effects:"fadeIn"
        });
    })
```



** 5.container ** :值为某容器.lazyload默认在拉动浏览器滚动条时生效,这个参数可以让你在拉动某DIV的滚动条时依次加载其中的图片  
```javascript
  $(function(){
        $("img.lazy").lazyload({
            container: $("#container") 
        });
    })
```


** 6.failure_limit **：一般用于当页面中图片不连续时使用，滚动页面的时候, Lazy Load 会循环为加载的图片. 在循环中检测图片是否在可视区域内，插件默认情况下在找到第一张不在可见区域的图片时停止循环。如：
```javascript
     $(function(){
        $("img.lazy").lazyload({
        failure_limit : 20
    });
 })
```

这里设为20表示插件找到 20 个不在可见区域的图片时才停止搜索。

** 7.skip_invisible **:为了提升性能，插件默认忽略隐藏的图片；如果想要加载隐藏图片.设置skip_invisible为false;
```javascript
     $(function(){
        $("img.lazy").lazyload({ 
        skip_invisible : false
    });
})
```

### -- echojs实现方式：
* 引入：在HTML中引入jQuery和jQuery-lazyload，如:
```html
<script type="text/javascript" src="js/echo.min.js"></script>
```
* 图片中的src使用data-echo代替如: 
```html
<img class="lazy" data-echo="images/p1.jpg" style="margin-top:500px" height="300">
```

* 添加js代码:
```javascript
echo.init({
//离可视区域多少像素的图片可以被加载
          offset: 500, 
 //图片延时多少毫秒加载
       　throttle: 1000
});
```


### -- echo只有两个可选参数：
* offset：离可视区域多少像素的图片可以被加载
* throttle：图片延时多少毫秒加载

## 最后说几句:
* 上述的懒加载实现方式都是人家实现好的，毕竟人家已经做好就不去重复造轮子，直接用人家会比较放心，因为大家都在用。
* jquery-lazyload插件的功能比较多，echojs虽然功能少但也基本够用，而且体积小，所以根据需求对两者取舍。
* 别人做好但也要去了解人家的如何去做，原理有了，我自己也尝试去做，写得还不是很好。这两个方式对于一些页面图片懒加载已经够用，但是对于轮播图的加载还是不够理想。  
* 遇到的一些问题:  
1.滚动轮播图片首次不能加载没有出现的图片。  
2.实现点击下一张轮播图才去加载那张图片。  
以上所说的这些还需要继续研究研究，正在寻求一些好的方法。

