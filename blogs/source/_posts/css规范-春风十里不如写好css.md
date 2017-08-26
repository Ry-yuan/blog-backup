---
title: css规范--春风十里不如写好css
date: 2017-08-18 15:59:33
tags: css
---
## 前言：
最近看了看春风十里不如你，本来很少看剧的，暑假有点闲就看了，感觉不错，挺喜欢这部剧，就套了个名字，嘿嘿嘿。剧里面印象深刻的是《致橡树》这首诗，念几句：
> 我如果爱你,绝不像攀援的凌霄花，借你的高枝炫耀自己;   
我如果爱你,绝不学痴情的鸟儿，为绿荫重复单调的歌曲；  
也不止像险峰，增加你的高度，衬托你的威仪。


不骚了，回到正题，写css也一样需要爱，你爱一门技术就要用心付出，对知识寸土必争，寸草必得。写css容易，写好就需要下功夫了。如果我爱你，就会去研究怎么去写好你，下面先说说怎么规范的写css。  
  
---
## css语法规范：
* 每条属性声明占一行，增加易读性
```
 /*bad*/
 body{margin: 0;padding: 0;}
 /*good*/
 body{
     margin: 0;
     padding: 0;
 }
```
* 颜色采用十六进制写法（不使用颜色名），并且能够简写的进行简写:
```
/*bad*/
.example{
    color: #ffaabb;
}
/*good*/
.example{
    color: #fab;
}
```
* 0值的单位进行省略，如将margin:0px，写成margin:0:
```
/*bad*/
.example{
    margin: 0px;
}
/*good*/
.example{
    margin: 0;
}
```
* 有选择器组时，每个选择器占一行：
```
  body,
  html,
  p{
      margin: 0;
      padding: 0;
  }
```

* 连字符使用-，而不使用_，因为能少按一个shift就少按，还有和js变量命名区分开。
```
/*bad*/
.index_list {}
/*good*/
.index-list {}
```
* 选择器避免使用标签名。(首先可能使得一些不必要的标签带上样式，其次会对选择器寻找上也会在一定程度上浪费时间)
```
/*bad*/
.index-list li{}
/*good*/
.index-list .item{}
```
* 媒体查询，不要写在文档最后或分开到另外文档，应该写在相应规则的附近，这样有利于修改和阅读
```
.index-nav{
    margin-top: 10px;
}
/*和相关的规则一起放*/
@media (min-width: 480px){
    .index-nav{
        margin-top: 5px;
    }
}
```
* 前缀，css3的一些属性要注意带上前缀：
```
.selector {
  -webkit-box-shadow: 0 1px 2px rgba(0,0,0,.15);
          box-shadow: 0 1px 2px rgba(0,0,0,.15);
}
```
* 引号方面，使用双引号而不使用单引号,url不用使用引号：
```
/*no good*/
.example{
    font-family: 'Times New Roman',Georgia,Serif;
    background: url("../images/icon.png");
}
/*good*/
.example{
    font-family: "Times New Roman",Georgia,Serif;
    background: url(../images/icon.png);
}
```
* 每条属性声明语句结束后加上分号，最后一条声明可省略分号，但不建议
* 每个属性声明的冒号（:）后添加一个空格
* 小于1的小数点的值，省略0，如0.5px，可写成.5px
* 避免使用@import指令，使用link标签来引入css文件
* 避免使用!important，这个优先级最高，滥用会使得维护困难，代码混乱
* Less,Sass等预处理言的嵌套不超过3层
* 避免使用id:(因为id优先级高，且具有唯一性，复用性差，而且id是html与js的挂钩，class是HTML与css的挂钩，这样能够让代码更为的清晰，不用说看到一个id，既要到js里查查有没有什么用，又到css里看看有什么样式，确实麻烦。)
* 注释需要全面易懂，不要只写一点  
    
  
---
## css属性声明顺序规范：
css属性的书写顺序大致分为4组，从上到下依次书写：
1.  Positioning Model（定位的相关属性）：
    * 有position，display，TRBL，z-index，float，overflow等
2.  Box Model （盒子模型的属性）：
    * 有margin，padding，border，width，height等
3.  Typographic （文本，排版）
    * 有font，line-height，text-align
4.  Visual （视觉方面的）
    * 有background，color，transition，list-style 
  
例子：
```
.example{
    content: "hello";
    /*positioning*/
    position: absolute;
    top: 10px;
    left: 12px;
    /*box model*/
    margin-top: 20px;
    width: 100px;
    heith: 100px;
    /*typographic*/
    text-align: center;
    font-size: 12px;
    /*visual*/
    color: #f00;
    background-color: #0f0;
}
```  
特别的：如果有content属性时，需要把其放到最前面     
    
---
## css的文件分类：
> 文件分类这不会有什么标准，分好，适合自己开发和维护便可。比如：可以有公共的css，某个页面的css，重置的css，皮肤的css，部件的css等，可根据自己的需求，习惯等分分类。不必太过拘束。  

* common.css（通用）
* main.css（主要）
* reset.css（重置）
* skin.css（皮肤）  
  

---
## css选择器命名：
命名这东西可以说让每个前端开发的人员苦恼的东西，有时得想半天去想一个名字，煎熬啊。老是想，到底怎么样的命名才比较好呢？我这样命名接着会不会重复？等等。。。  
到底怎样命名才比较规范，参考一下NEC规范或者是BEM规范。个人比较喜欢NEC，因为其比较简约些,详细的可以到NEC官网上看看。
看看NEC的分类：
* 布局（grid）（.g-）：将页面分割为几个大块，通常有头部、主体、主栏、侧栏、尾部等！
* 模块（module）（.m-）：通常是一个语义化的可以重复使用的较大的整体！比如导航、登录、注册、各种列表、评论、搜索等！
* 元件（unit）（.u-）：通常是一个不可再分的较为小巧的个体，通常被重复用于各种模块中！比如按钮、输入框、loading、图标等！
* 功能（function）（.f-）：为方便一些常用样式的使用，我们将这些使用率较高的样式剥离出来，按需使用，通常这些选择器具有固定样式表现，比如清除浮动等！不可滥用！
* 皮肤（skin）（.s-）：如果你需要把皮肤型的样式抽离出来，通常为文字色、背景色（图）、边框色等，非换肤型网站通常只提取文字色！非换肤型网站不可滥用此类！
* 状态（.z-）：为状态类样式加入前缀，统一标识，方便识别，她只能组合使用或作为后代出现（.u-ipt.z-dis{}，.m-list li.z-sel{}）

> 我们参考NEC的分类命名的规范，学习学习它的命名，可以照着使用，也可以有自己不同的命名，可以根据团队的习惯等。规矩是死的，人是活的，能灵活去变通才是最好的，能够写出清晰易懂的代码就ok。  

---

## css命名常用单词：
* 头：header 
* 尾：footer 
* 导航：nav 
* 侧栏：sidebar 
* 栏目：column 
* 外围容器：wrapper 
* 登录条：loginbar 
* 标志：logo 
* 广告：banner 
* 页面主体：main 
* 热点：hot 
* 新闻：news 
* 下载：download 
* 子导航：subnav 
* 菜单：menu 
* 子菜单：submenu 
* 搜索：search 
* 友情链接：friendlink 
* 页脚：footer 
* 版权：copyright 
* 滚动：scroll 
* 内容：content 
* 标签页：tab 
* 文章列表：list 
* 信息：msg 
* 小技巧：tips 
* 标题：title 
* 加入：joinus 
* 指南：guild 
* 服务：service 
* 注册：regsiter 
* 状态：status 
* 投票：vote 
* 合作伙伴：partner
* 容器：container
* 按钮：button

> 单词这方面能看懂就好，英语也要学号才行啊，有时候不懂怎么命名，就查查英文单词怎么写，看得出英语还是很重要啊。css的命名单词长度不要太长太冗余，看懂就好，有些单词过长可以适当的缩写一下。

## 最后说说：
> 如果想学好一门技术，就想要从各个方面研究他，本文也是，了解css也要css的规范，这对于强迫症的人就是很好的疗药，我就是这样，总觉得自己的css写得太不规范，也不容易维护，想要去修饰好，所以写写博客来强迫自己去改正，博客是个好东西，写给自己看看同时也写给别人看，所以这会有约束，从而不断的修饰改正错误，从中自己也会学到很多东西，可谓春风十里不如写博客。
