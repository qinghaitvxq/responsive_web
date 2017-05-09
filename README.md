# 响应式设计 - 让内容来决定
###什么是响应式思维 ？
 ######  即考虑用户在任何设备上的体验。
> * 如果设备是某种尺寸的手机，我希望用户看到什么？

 >* 如果设备是平板，我希望用户看到哪些元素？
 >* 如果设备是电脑，我的页面应该是什么样子的？

######你需要考虑的问题很多，推荐的思考顺序是：
 >* 设计时我们应该从从最小的屏幕，逐步推进到更大的屏幕
 >* 开发时我们从大块的布局开始，逐步推进到元素的优化
 
 **设计 - 从小到大**
>![Paste_Image.png](http://upload-images.jianshu.io/upload_images/4323852-6a899a8276e6b17d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 设计响应式网页的概念和过程和非响应式的是一样的。只不过他要画多种宽度的设计稿来适应不同屏幕尺寸。通常设计是从最小的屏幕开始做起，比如手机设备，然后下一个做更大的。从最小的屏幕做起，一般我们要考虑对于用户来说，什么是最重要的。如果从最大的屏幕开始设计，就有可能在缩减的过程中轻易删除掉一些重要的信息。**从小到大的设计，能保证最重要的内容永远都在页面上**。

 **开发 - 从大到小**

 开发时，在确定布局之后，要考虑小屏幕设备上互动的方便性。在PC端，我们使用鼠标时，是可以**精确**地点击元素。而如果使用我们的手指，操纵的精确度就会很糟糕。我们的手指大约有 10mm  宽，约等于 40 个CSS像素。一般我们可以把按钮尺寸设计为 48px*48px , 这样就能确保元素之间有足够的距离，以及那些手指更粗的人也能使用。有时候，敲击目标设计得小一些也OK ,但是请确保任何两个敲击目标之间至少有40px的距离。这样能放置用户同时点击到两个按钮。
响应式按钮的推荐CSS姿势如下：
   ```
   nav a , button{
       min-width : 48px ;
       min-height : 48px ;
}
```


###怎么来实现响应式 ？
#####响应式实现要点之一：viewport（视图窗口）
```
 <meta name=" viewport " content=" width=device-width,initial-scale=1 ">
```

** 首先有几个关于尺寸的概念简单说明一下：**

* 屏幕尺寸 
    用户设备屏幕的大小，是显示器的属性，值不变 。javascript  可以通过 screen.width  和  screen.height 获取。

>* 窗口尺寸
 浏览器窗口的整体大小。大小随着浏览器窗口大小的改变而改变。javascript   可通过 window.innerWidth 和 window.innerHeight 来获取这些尺寸。 (浏览器上打开DevTools , Console上可直接做实验）

>* viewport
用来约束你网站中最顶级包含块元素（containing block）<html>。实际上等于窗口尺寸，即**浏览器能够显示内容的区域**


   为 head 元素添加 viewport 标签，可以让浏览器知道我们的意图。我们需要在视窗值后面设置页面宽度，来指导页面针对具体设备进行宽度调整，这使页面内容可以匹配不同屏幕尺寸。initial-scale 是浏览器相对像素与CSS像素的比例。如果不把初始缩放比例设置为1的话，有的浏览器会在切换到横屏模式时，依旧保持之前的页面宽度，而且它们还会使内容只是进行缩放，而无法自动调整布局。


#####响应式实现要点之二：媒体查询

响应式网页会基于设备的特征而变化。也就是说你的响应式网页在不同的设备上需要应用不同的样式，我们可以通过媒体查询来实现。
> **媒体查询**
  提供简单的逻辑方法，根据不同的设备特征应用不同样式，比如设备的宽度、高度或像素比。

添加响应式样式很简单，一般有以下三种方式。
1. 文件层面。页面上添加另外的样式表，并附上媒体查询。比如，我们有一个样式，只有当屏幕宽度大于 500px 时它才生效。
```
<link rel=" stylesheet "   media=" screen and ( min-width:500px ) "   href=" over500.css " >
```
* 文件层面。和上面原理基本类似，但由于性能原因，不建议使用。
```
@import url ( "no.css" ) only screen and (min-width : 500px )
（性能原因,不推荐使用）
```
* 代码块
```
@media screen and ( min-width : 500 px){
    body { background-color : green ; }
}
```

媒体查询变量有很多个，感兴趣的可以自己查一查。最常用的是 min-width 和 max-width。max-width 下的规则在视图宽度小于其赋值时生效，
min-width 下的规则在视图宽度大于其赋值时生效。

**做个小练习（practise makes perfect）**
有一个简单的html页面，要求如下:
1. 在 0-400px 时，背景为红色
2. 401-599px 时，背景为绿色
3. 大于等于600px 时，背景为蓝色

读者们可以动手试一试，如果没用过媒体查询的语法，写一下印象会更深刻。有个小提示，chrome打开开发者工具，改变当前浏览器窗口大小时可以即时看到当前窗口宽度。
>![Paste_Image.png](http://upload-images.jianshu.io/upload_images/4323852-5dcc7383e97e0a5f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
练习比较简单，注意每个条件使用的查询属性即可。
```
        body{
            background-color: green;
          }
        @media screen and (max-width:400px){
            body{
                background-color: red;
            }
        }
        @media screen and (min-width:600px){
            body{
                background-color: blue;
            }
        }
```

**That's All ? **

Actually.......yes ! 响应式布局用到的核心技术基本上就是这两点了。是不是很简单？但是感觉用这个啥也做不了啊？其实复杂的东西都是由简单的东西组成的。响应式的核心技术并不复杂，只不过它组合了一些页面展示策略、CSS的效果，从而产生了各式各样令人惊叹（...可能夸张了...）的效果。

#### 常见响应式设计模式
在介绍常见的设计模式之前，响应式布局中有一个重要的概念需要先介绍一下。

#####断点（breakpoint）
 > 页面改变布局的那个点叫做**间断点**  。
一个页面上可以有一个或多个间断点，间断点的选择**没有绝对的答案**，我们应该**根据网页的内容来找寻找到合适的间断点**。可以这么认为，在选择间断点上，感性 > 理性 。

一般推荐的寻找方法是，从最小版本的设计开始，打开开发者工具，以便查看实时的分辨率。然后慢慢地拉大窗口，在你感觉页面的某些元素之间有超出一般空旷的空间时或者其他原因让你感觉当前的页面布局需要改变一下的时候，此时浏览器右上方显示的那个宽度便是你找到的 “ 断点 ” 。记住，**我们要让网页的内容告诉我们，它需要断点的位置**。

#####三个常见的响应式设计模式
*  列坠落   （Column Drop  ）
*  布局切换  （Layout Shifter） 
*  画布溢出 （off Canvas）


######Column Drop 
>![image.png](http://upload-images.jianshu.io/upload_images/4323852-193f1b5217591c09.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**说明**
1. 在视图最窄的时候，每个元素都纵向堆放，
2. 当视图变宽，元素也随之延展，直至到达第一个间断点。
3. 在第一个间断点，所有元素不再竖直堆放，而是前两个元素并排显示，第三个元素放在下面。
4. 视图继续变宽，直至到达下一个间断点，它们会重新排列成一个三列的布局。
5. 当视窗达到最大宽度，列也达到最大的宽度时，它们便不再随视窗延展，而是在两侧添加外边距。

这里我们会通过flexbox来实现 , 简单说明一下flexbox的原理。
> * flexbox 的强大在于它能够**自动填充空白区域**，如果一个元素周围出现了空白，它会自动填补上。而如果空间变得拥挤，它会缩小，直至占据最小空间。flex默认的堆放方式是**横向堆放 ( 这里注意浏览器对块状元素的默认布局是竖直，即不在同一行)**，默认情况下，flex项目会自动填充在一行内，无论将元素的宽度设为多少，它们都不会换行。相反，浏览器会调整它们的尺寸以适应窗口的大小。

>* 如果给container元素添加flex-wrap:wrap语句，则是告诉浏览器允许内部元素换行。

>* 可以利用CSS order属性来改变元素的次序。

对于以上的响应式要求，我们首先确定基本的元素顺序，然后通过媒体查询在不同的页面宽度下改变元素的宽度。( 这里会给出核心代码，若想要查看所有的源码，可以在文章底部的链接地址中获取 ）
```
基本布局：
  <div class="container">
      <div class="box dark_blue"></div>
      <div class="box light_blue"></div>
      <div class="box green"></div>
  </div>
css:
<style>
   .container{
            display:flex;
            flex-wrap:wrap;
        }
    @media screen and (min-width:450px){
            .dark_blue{
                width:25%;
            }
            .light_blue{
             width:75%;
            }
        }
    @media screen and (min-width:550px){
           .green,.dark_blue{
               width:25%;
           }
            .light_blue{
                width:50%;
            }
        }
    @media screen and (min-width:700px){
            .container{
                width:700px;
                margin-left:auto;
                margin-right:auto;
            }
        }
</style>
```


######  Layout Shifter 活动布局 
活动布局模型应该是最灵活的响应式模型了，它有很多适用于不同设备的间断点。但最关键的是它的布局变化方式。
>![image.png](http://upload-images.jianshu.io/upload_images/4323852-186503f8658bce14.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

注意看上图红色的部分，它不再是单纯地重排到其他列的下方，在第三个布局中，它是页面的第一个元素。这里凸显了flexbox的亮点，它利用了CSS的**order属性**。注意这样一来，每个布局可变化的地方就很多了，当然你需要写更多其他的css代码来实现。比如，中间浅蓝色和绿色的行为基本上是一致的，那么合理的方式是给这两个一个相同的父元素。
```
布局
<div class="container">
    <div class="box dark_blue">
    </div>
    <div class="container" id="container2">
        <div class="box light_blue"></div>
        <div class="box green"></div>
    </div>
    <div class="box red"></div>
</div>

CSS:
<style>
     .container{
            width:100%;
            display:flex;
            flex-wrap:wrap;
        }
      @media screen and (min-width:500px){
            .dark_blue{
                width:50%;
                height:200px;
            }
            #container2{
                width:50%;
            }
        }
      @media screen and (min-width:600px){
            .dark_blue{
                width:25%;
                order:1;
            }
            #container2{
                width:50%;
            }
            .red{
                width:25%;
                order:-1;
                height:200px;
            }
        }
</style>
```

##### off Canvas 画布溢出

在off Canvas 模型中，内容并不是竖直堆放的。而是将不常用的内容，比如导航栏或者应用菜单放在屏幕以外，只有当屏幕足够大的时候才显示出来。在小尺寸的屏幕上，溢出画布的内容通常会在用户点击菜单按钮时出现。

>![image.png](http://upload-images.jianshu.io/upload_images/4323852-165c1fd34ca9895a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这个响应式的实现主要是针对导航部分的位置（position）做文章，核心代码如下：
```
 nav {
        width: 300px;
        height: 100%;
        position: absolute;
        /* This trasform moves the drawer off canvas. */
        -webkit-transform: translate(-300px, 0);
        transform: translate(-300px, 0);
        /* Optionally, we animate the drawer. */
        transition: transform 0.3s ease;
    }
 @media (min-width: 600px) {
        /* We open the drawer. */
        nav {
            position:relative;
            -webkit-transform: translate(0, 0);
            transform: translate(0, 0);
        }
        /* We use Flexbox on the parent. */
        body {
            display: -webkit-flex;
            display: flex;
            -webkit-flex-flow: row nowrap;
            flex-flow: row nowrap;
        }
        main {
            width: auto;
            /* Flex-grow streches the main content to fill all available space. */
            flex-grow: 1;
        }
    }

```

#####次要断点
除了选择主要断点，即布局显著改变的地方，增加副断点来实现一些小的改变是很有帮助的，比如在主要断点之间调整元素的外边距和内边距可能会很有帮助。或者给一些内容增加字号，会更容易阅读。次要断点设置得好，可以给你的响应式增加很多小惊喜。