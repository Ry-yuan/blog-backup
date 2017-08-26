---
title: 前端性能优化--图片处理（Css Sprites 和 base64）)
date: 2017-08-19 16:09:37
tags: 前端性能优化
---
## 前言：  
> 近期研究着前端性能的优化方面的知识，并以博客记之。之前已有相同系列的文章（[前端性能优化--图片懒加载(lazyload image)](http://www.cnblogs.com/Ry-yuan/p/7232109.html)），这次继续是关于图片的处理，**css sprites** 和 **base64** 格式图片，这两种处理都是通过减少了http的请求来达到前端性能优化的效果，请求减少，与服务器连接次数减少，加载页面的时间就快了，如是甚好。  
  
---
## Css Sprites：
### 介绍：
Css Sprites（雪碧图或css精灵），是网页图片处理的一种方式，它允许你将一个页面涉及到的所有零星图片都包含到一张大图中去，这样一来，当访问该页面时，载入的图片就不会像以前那样一幅一幅地慢慢显示出来了。 

### 原理：
将许多的小图片整合到一张大图片中，利用css中的background-image属性，background-position属性定位某个图片位置，来达到在大图片中引用某个部位的小图片的效果。
### 优点：
* 减少网页的http请求，提升网页加载速度。
* 合并多张小图片成大图，能减少字节总数（大图大小<=多张小图大小）.  

### 缺点：
* 前期需要处理图片将小图合并，多些许工程量。
* 对于需要经常改变的图片维护起来麻烦。

### 应用例子：
* 生成雪碧图：我这里使用了**网页雪碧图制作专家**，当然还有很多其他的工具
* 合成的图片如图所示：  
![](http://images2017.cnblogs.com/blog/1144006/201708/1144006-20170819180554693-282102268.jpg)  
  
html代码：
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>css Sprites</title>
</head>

<body>
    <ul class="container">
        <li class="icon icon-issue"></li>
        <li class="icon icon-upload"></li>
        <li class="icon icon-passage"></li>
    </ul>
</body>

</html>
```
  
css代码：
```html
.container {
    overflow: hidden;
    width: 50px;
    height: 200px;
    background-color: #faa755;
}

.icon {
    margin: 0 auto;
    margin-top: 20px;
    width: 40px;
    height: 30px;
    background-image: url(icon.png);
    list-style-type: none;
}

.icon-issue {
    background-position: 0 0;
}

.icon-upload {
    background-position: 0 -50px;
}

.icon-passage {
    background-position: 0 -100px;
}
```
  
* 效果图：
![](http://images2017.cnblogs.com/blog/1144006/201708/1144006-20170819180319490-1730910425.jpg)



### 适用场景：
* 对于一些不需要多变动的小图片，表情，标志等等都可以使用。  
* 一般都是应用于小图片，太大的图片不利于合并，且定位麻烦，一次的加载时间长，导致全部图片出现时间延迟，效果不友好。   
   
---  

## base64：
#### 介绍：
base64是网络上最常见的用于传输8Bit字节代码的编码方式之一，要求把每三个8Bit的字节转换为四个6Bit的字节，Base64是网络上最常见的用于传输8Bit字节代码的编码方式之一。

通俗点讲：将资源原本二进制形式转成以64个字符基本单位，所组成的一串字符串。  
比如一张图片转成base64编码后就像这样，图片直接以base64形式嵌入文件中（很长没截完）：
![](http://images2017.cnblogs.com/blog/1144006/201708/1144006-20170819180913521-1207813845.jpg)
#### 生成base64编码：
图片生成base64可以用一些工具，如在线工具，但在项目中这样一个图片这样生成是挺繁琐。webpack中的url-loader可以完成这个工作，可以对限制大小的图片进行base64的转换，非常方便。
#### 优点：
1.base64的图片会随着html或者css一起下载到浏览器,减少了请求.
#### 缺点：
1.低版本的IE浏览器不兼容。  
2.体积会比原来的图片大一点。  
3.css中过多使用base64图片会使得css过大，不利于css的加载。
#### 应用场景：
1.应用于小的图片几k的，太大的图片会转换后的大小太大，得不偿失。  
2.用于一些css sprites不利处理的小图片，如一些可以通过background-repeat平铺来做成背景的图片。

## 收收尾：
>上面说的两个处理图片共同点是都是应用于小图片，都能减少请求数，但并不是所有的图片都适用，尺寸大的图片就不应使用。    
两种方式都有利有弊，应该适应场景使用，权衡利弊，方可将这两种方法能力发挥好。 
鄙人才浅，若有疏漏之处，欢迎指出。 