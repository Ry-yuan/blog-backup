---
title: css之定位布局
date: 2017-05-11 19:26:54
tags: css
---
### css之定位布局(position,定位布局技巧)
#### 1.什么是定位
css中的position属性，position有四个值：absolute/relative/fixed/static(绝对/相对/固定/静态(默认))通过定位属性可以设置一些不规则的布局，使用TLBR(top,left,bottom,right)来调整元素位置。
#### 2.各个属性值的描述：
1.static(静态) 没有特别的设定，遵循基本的定位规定，不能通过z-index进行层次分级，在普通流中，各个元素默认的属性。
2.relative(相对定位) 对象不可层叠、不脱离文档流，参考自身静态位置通过 top,bottom,left,right 定位。
3.absolute(绝对定位) 脱离文档流，通过 top,bottom,left,right 定位。选取其最近一个最有定位设置的父级对象进行绝对定位，如果对象的父级没有设置定位属性，absolute元素将以body坐标原点进行定位。
4.fixed（固定定位） 这里所固定的参照对像是可视窗口而并非是body或是父级元素。使用了fixed的元素不会随着窗口的滚动而滚动。属于absolute的子集。
#### 3.各个属性值的具体作用：
A.**static**：（静态，默认的属性）通常情况下都不会使用，但是会存在有些场景，就是你想把position的值从其他值修改成默认时使用。

B.**relative**：（相对定位）一个元素设定了position:relative，因为其不脱离文本流，如果不设置TLBR(top,left,bottom,right)的话，它的位置不会被改变，且不会影响当前布局，相当于没事发生一样。如果设置了TLBR后，元素就可以向指定的方向偏移，但是他原有的位置还是占据着的，例子如图：
图一：对child-1 设置了position：relative
![p1](/img/p1.png)
图二：再对child-1 调位置 top：20px left：20px
![p2](/img/p2.png)
C.**absolute**: (绝对定位)，完全脱离文本流（普通流），原来的位置不再占有，且可以设置TLBR任意移动；

特别说明一下，对元素设置了absolute后，其父级元素都没有设置position：absolute/relative/fixed其会以body为父级。

图一：
![p3](/img/p3.png)
图二：
![p4](/img/p4.png)
图三：
![p5](/img/p5.png)
D.**fixed**：(固定定位),不会随着页面滚动而滚动，这里就不贴图了，最形象的就是那些网页小广告，你滚动页面，但是它一直在网页的右边或左边，死跟着你。

#### 4.定位布局技巧：position：relative 与 position：absolute 结合使用:
上面提到如果对元素设置了absolute后，其父级元素都没有设置position：relative，其会以body为父级。这样的话我们该元素定位到我们的目标位置将很困难，量像素麻烦。图片说明：
图一：初始状态
![p6](/img/p6.png)
图二：对box-chd-chd设置position：absolute 并设置 top：0， left:0 可以看到它从body作为父级，会以最左上角作为起点
![p7](/img/p7.png)
图三：对box 设置position：relative，可以看到此时box-chd-chd以box作为父级
![p8](/img/p8.png)
图四：再对box-chd 设置position：relative，可以看到box-chd-chd以box-chd作为父级
![p9](/img/p9.png)
可以看出，当子代设置了position：absolute后，其父级那个设置了position：relative，这个子代就会从该父级元素最左上方作为起点移动，并且遵循就近原则，即子代向上找父级，当找到第一个有父级设置了relative就以它最左上方作为起点。
relative 与 absolute 结合的方式，对定位布局起到了便利，需要移动的距离也得到缩小，不用从body开始整个页面来量取像素，同时也方便管理，结构清晰。
 
总结：上一篇写了float的布局技巧，这章是position，可以看出position与float都是一种布局方式，且各有各的应用场景，可以根据需求来选择布局方式。
作者：Ry-yuan
如需转载请标明出处，原文地址：http://www.cnblogs.com/Ry-yuan/p/6822619.html