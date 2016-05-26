[TOC]

## 基础知识总结

### CSS总结

#### 基础CSS

CSS本质可以分为宏观和微观两部分。宏观上它的存在就是为了控制页面的显示样式，包括布局，颜色，字体等。微观上则是实现这种控制功能的各种属性的定义和工作原理。

常用基础样式：

![常用基础样式][img1]

详细解释：

* 布局
    - float : 
        浮动的元素可以向左或向右移动，直到外边缘碰到包含元素或另一个浮动元素的边框为止。浮动的元素脱离文档流，文档流中其他元素忽视它。  
        浮动元素会生成一个块级框，无论它是什么元素，都会转成块级元素。需要宽度。  
        + right  向右浮动
        + left  向左浮动
        + none  默认值，不浮动。显示在文档流中的正常位置
        + inherit  从父元素继承float属性的值()
    - clear : 清除浮动
        + right : 清除右侧的浮动元素
        + left : 清除左侧的浮动元素
        + both : 清除左右两侧
        + none : 默认值，允许浮动元素出现在左右两侧
        + inherit : 从父元素继承(任何版本的IE都不支持inherit)
    PS : 当想让图片浮动到文本的左边，且 **图片和文本包含在另一个具有边框和背景的div中** 。有两种办法 :
    1. 把包含div(父div)也设置为浮动。但这样会使后面的元素受到影响。
    2. **在包含div中再添加一个空div，为这个div设置清除浮动**
    - display: 规定元素应该生成的框的类型
        + none : 此元素不会被显示
        + block : 显示为块级元素，前后都有换行符
        + inline : 显示为行内元素，前后没有换行符
        + inline-block : 行内块元素
        + inherit : 从父元素继承
    PS:display:none 与 visible:hidden 的区别:  
    **display:none** 不为被隐藏的对象保留物理空间，“看不见也摸不到”  
    **visibility:hidden** 是对象在网页上不可见，但它的物理空间没有消失。

    - position:
        CSS有三种基本的定位机制：文档流，浮动，定位  
        文档流就是按照元素在文档中的顺序进行排列，块级元素从上到下排列，元素与元素之间的 **垂直距离由垂直外边距计算出来** 。行内元素在行中水平排列，可以使用 **水平内边距，边框和外边距** 调整它们的间距。但垂直内边距，边框和外边距 **不影响** 行内框的高度。
        **行框的高度总是足以容纳它包含的所有行内框。** 不过可以通过定义 **行高(line-height)** 来改变行框的高度。
        + static : 默认值，没有定位。元素出现在正常的文档流中(忽略'top','right','bottom','left','z-index'属性 )
        + relative : 生成相对定位，相对于原来的位置进行定位。**元素的位置通过'top','right','bottom','left'属性进行定位** 
        + absolute : 元素从文档流中删除，生成绝对定位的元素。相对于 **static定位以外的第一个父元素**定位。 **元素的位置通过'top','right','bottom','left'属性进行定位** 
        + fixed : 生成绝对定位，相对于浏览器窗口进行定位。**元素的位置通过'top','right','bottom','left'属性进行定位** 
        + inherit : 规定从父元素继承position属性
    - top: 规定元素的顶部边缘。定位元素的上外边距边界与其包含块的上边界之间的偏移
    - right: 定义了定位元素右外边距边界与其包含块右边界之间的偏移。
    - bottom: 定义了定位元素下外边距边界与其包含块下边界之间的偏移。
    - left: 定义了定位元素左外边距边界与其包含块左边界之间的偏移。
    - overflow: 当内容溢出元素框时发生的事情。  
        + visible : 默认值，内容不会被修剪，出现在元素框之外
        + hidden : 内容会被修剪，超出的内容会被隐藏，不可见。
        + scroll : 内容会被修剪，浏览器会显示滚动条来查看超出的内容
        + auto : 如果内容内修剪，浏览器就会显示滚动条来查看超出的内容
        + inherit : 从父元素继承overflow的属性值
    - clip-path: 根据二维点坐标，依次连线，最后形成的区域就是遮罩区域。 !点的顺序一定要能连成一个多边形
        + polygon(0 100%,50% 0,100% 100%);   //多边形函数，参数为几个点的坐标(此行的效果是三角形)    
        + circle(50% at 50% 50%); //圆形函数,参数为圆的半径和圆心的坐标(at前面是半径,at后面是坐标)  
        + ellipse(30% 20% at 50% 50%);    //椭圆函数，参数为x轴半径，y轴半径，at后面是圆心坐标  
        + inset(25% 0 25% 0 round 0 25% 0 25%);  //带圆角的多边形,参数是上，右，下，左 round 上角，右角，下角，左角(可以简写)
    - z-index: 设置元素的堆叠顺序(元素可拥有负的z-index值)
        z-index值高的排在z-index值低的前面
        **z-index值仅能在定位元素上奏效！**
        + auto : 默认，堆叠顺序与父元素相等
        + *number* : 设置元素的堆叠顺序
        + inherit : 从父元素继承z-index属性的值
* 盒模型 
    ![盒模型概述][img2]
    PS:盒模型分为W3C标准盒模型和ie盒模型  
    W3C标准盒模型包括：margin,border,padding,content,并且 **content部分不包含其他部分** 。  
    IE盒模型也包括margin,border,padding,content,但 **content部分包括border和padding** 。  
    在文档头部加上`<!DOCTYPE html>`声明,就会按W3C标准盒模型来解析。
    - width: content区域的宽度
    - height: content区域的高度
    - padding: 内边距 (元素内容与元素边框间的空白区域， **不允许负值** )
    - margin: 外边距 (margin在元素外创建额外的空白, **可以是负值** ，很多情况下都会用到margin的负值)
    PS : 当值为百分比时，百分数值相对于其父元素的width计算的
    - 外边距合并 ( **当两个垂直外边距相遇时，它们将形成一个大外边距。合并后的外边距的高度等于；两个发生合并的外边距中高度较大者** )
    PS : 只有 **普通文档流** 中 **块框** 的 **垂直外边距** 才会发生外边距合并， **行内框** ， **浮动框** 或 **绝对定位** 之间的外边距不会合并。
    - border: 边框 (有三个方面，宽度，样式，颜色)
        + border-style (样式)
            * none 无边框
            * hidden 
            * dotted 点状边框。大多数浏览器中呈现实线
            * dashed 虚线。大多数浏览器中呈现实线
            * solid 实线
            * double 双线
            * groove 3D凹槽边框，效果取决于`border-color`
            * ridge 3D垄状边框
            * inset 3Dinset边框
            * outset 3Doutset边框
            * inherit 从父元素继承
        PS:可以为四条边分别设置`border-top-style`,`border-right-style`...
            合写顺序为 **上右下左**
        + border-width (宽度) 只有style不是none时才起作用
            * thin 细的
            * medium 默认 中等宽度
            * thick 粗的
            * *length* 数值
            * inherit 从父元素继承
        + border-color (颜色)
            * transparent 默认 透明
    PS : 背景应用于content和padding、border组成的区域
* 颜色、背景
    - color : 字体颜色
    - background: 
        + -color: 默认值 transparent 透明 可以为所有元素设置背景色，包括 **行内元素** 
        + -image: 
            * url('URL') 指向图像的路径
            * none 默认值 不显示背景图像
            * inherit 从父元素继承
        + -repeat: **设置是否及如何重复背景图像**
            * repeat 默认值 背景图像在水平和垂直方向重复
            * repeat-x 在水平方向上重复
            * repeat-y 在垂直方向上重复
            * no-repeat 不重复
            * inherit 从父元素继承
        + -position: **设置背景图像的起始位置** 
            * 方位值 : 两个参数 表示水平方向的方位(left center bottom) 表示垂直方向的方位(top center bottom) **当仅设置一个值时，第二个值默认为center**
            * x% y% : 第一个值是水平位置 第二个值是垂直位置 左上角是0% 0% 右下角是100% 100% 如果仅规定一个值，第二个值是50%
            * 像素值 像素值 : 第一个值是水平位置 第二个值是垂直位置 可以与百分比混用。
        + -attachment: **设置固定的背景图像**
            * scroll 默认值 背景图像随着其余部分的滚动而移动
            * fixed 当页面其他部分滚动时，背景图像不会移动
            * inherit 从父元素继承
        + -size: **规定背景图像的尺寸**
            * *length* 宽度和高度。如果只设置一个值，后一个值为auto
            * 百分比 以父元素的百分比来设置背景图像的宽度和高度
            * cover 把背景图像扩展至足够大，时完全覆盖背景区域，有些部分可能无法显示在背景定位区域中
            * contain 把图像扩展至最大在尺寸，**使宽度和高度完全适应内容区域**
        + -clip: **规定背景的绘制区域**
            * border-box 背景被裁剪到边框盒(背景区域content+padding+border)
            * padding-box 背景被裁剪到内边距盒(背景区域content+padding)
            * content-box 内容盒(背景区域只有content)
        + -origin: **规定background-position属性相对于什么位置来定位**
        PS : 当background-attachment值为fixed时，此属性失效
            * border-box 相对于边框盒
            * padding-box 相对于内边距盒
            * content-box 相对于内容盒子
* 字体
    - -family:
        font-family规定元素的字体系列。可以把多个字体名称(用逗号分隔)作为一个回退系统来保存，如果浏览器不支持第一个字体，会尝试下一个，也就是说浏览器会使用它可识别的第一个值。
        + 指定的系列名称：具体的字体名称，比如'times','couier','arial'
        + 通常字体系列名称：'serif','sans-serif','cursive','fantasy','monospace'
        PS : 只有当肢体名中有一个或多个空格，或者如果字体名包括#,$之类的符号，才需要在font-family声明中加引号。
    - -weight : 设置文本的粗细
        + normal 默认值 标准粗细
        + bold 定义粗体字符
        + bolder 定义更粗的字符
        + lighter 定义更细的字符
        + *number* 100~700 由细到粗
        + inherit
    - -size : 文本的大小
        + 绝对值 
            * 将文本设置为指定的大小
            * 不允许用户在所有浏览器中改变文本大小
            * 绝对大小在输出的物理尺寸确定时和有用
        + 相对大小
            * 相对周围元素设置大小
            * 允许用户改变
        PS : 如果没有规定字体大小，普通文本(段落)的大小是16px(1em)
        PPS : 1em 等于当前的字体尺寸
    - -style : 定义字体的风格
        + normal 默认值 浏览器显示一个标准的字体样式
        + italic 斜体(斜体是一种字体风格)
        + oblique 倾斜(倾斜是正常竖直文本的倾斜版)(通常情况下，它俩看上去一样)
        + inherit 从父元素继承
    - -variant : 定义小型大写字母文本(所有小写字母会转换成大写，但与其余文本相比更小)
        + normal 默认值
        + small-caps 小型大写字母
        + inherit 从父元素继承
* 文本
    - text-indent : 文本块中首行文本缩进(允许负值，那么首行会被缩进到左边，此时文本有可能会超出浏览器边界，最好设置个外边距或内边距)
        + *length* 固定的缩进，默认值0
        + % 基于 **父元素宽度** 的百分比缩进
        + inherit
    - text-align : 文本的水平对齐方式
        + left 默认值 文本排列到左边
        + right 文本排列到右边
        + center 居中
        + justify 实现两端对齐文本效果
        + inherit
    - line-height : 行高
        + normal 
        + *number* 数字会与当前字体尺寸相乘来计算行高
        + length 设置固定的行间距
        + %
        + inherit
    - vertical-align: 设置元素的垂直对齐方式
        定义行内元素的基线相对于该元素所在行的基线的垂直对齐。允许指定负长度值和百分比值。这会使元素 **降低而不是升高** 
        + baseline : 默认值，元素放置在父元素的基线上。
        + sub : 垂直对齐文本的下标
        + super : 垂直对齐文本的上标
        + top : 把元素顶端与行中最高元素的顶端对齐
        + text-top : 把元素的顶端与父元素字体的顶端对齐
        + middle : 把此元素放在父元素中部
        + bottom : 把此元素顶端与行内最低元素的顶端对齐 
        + text-bottom : 把元素底端与父元素字体的底端对齐
        + inherit : 从父元素继承visible-align属性值
    - word-spacing : 改变单词之间的空间间隔
        + normal 默认值
        + *length* 固定空间
        + inherit
    - letter-spacing : 字符间距
        + normal 默认值 无间距
        + *length*
        + inherit
    - text-transform : 控制文本的大小写
        + none 默认值
        + capitalize 每个单词以大写字母开头
        + uppercase 全变成大写
        + lowercase 全变成小写
        + inherit
    - text-decoration : 添加到文本上的修饰(修饰的颜色由color属性设置)
        + none 默认值
        + underline 定义文本的一条下划线
        + overline 定义文本上的一条线
        + line-through 穿过文本的一条线
        + blink 闪烁的文本
        + inherit
    - white-space : 如何处理元素中的空白
        + normal 
        + pre 空白被浏览器保留，类似于HTML中的 < pre > 标签
        + nowrap 文本不换行
        + pre-wrap 保留空白符序列，但正常的换行
        + pre-line 合并空白符序列 但是保留换行符
        + inherit
    - direction : 块的文本方向
        + ltr 默认 从左到右
        + rtl 从右到左
        + inherit

#### CSS高级

##### 对齐

* 使用margin属性来水平对齐
    `margin:0 auto` 左右外边距设置为auto(如果宽度是100%，对齐无效果)
* 使用position属性来左和右对齐
    绝对定位 `position:absolute`(绝对定位元素会被从正常流中删除，并且能够交叠元素)
* 使用float属性进行左和右对齐
    `float:right;`
PS : <!DOCTYPE html>一定不要忘记

##### 导航栏

导航栏基本上是一个链接列表，所以用< ul >和< li >非常合适

```
ul{ /*去掉圆点和边距*/
    list-type-style : none;
    margin : 0;
    padding : 0;
}
```

水平导航栏 

    li { float : left; } /*对列表项进行浮动*/

##### 图片透明

IE9、Firefox、Chrome、Opera和Safari使用属性 `opacity` 来透明度，从0.0到1.0

#### CSS3

##### 边框

* border-radius
    - 圆角边框(设置边框四个角的弧度)
    - 上右下左或简写
    - px 或 %
* box-shadow
    - 阴影边框(向框添加一个或多个阴影)
    - 每个阴影由2-4个长度值、可选的颜色值、及可选的inset关键词来决定，省略的长度值是0
    - h-shadow(水平阴影的位置) 必需 允许负值
    - v-shadow(垂直阴影的位置) 必需 允许负值
    - blur(模糊距离) 可选
    - spread(阴影的尺寸) 可选
    - color(阴影的颜色) 可选
    - inset(可将外部阴影改为内部阴影) 可选
    - 例 : box-shadow:10px 10px 5px 5px blue inset;(水平位置，垂直位置，模糊距离，阴影尺寸，颜色，内部阴影)
* border-image
    - 用于边框的图片
    - URL 图片路径
    - 内偏移
    - 图片边框的宽度
    - 边框区域超出边框的量
    - 图像边框是否应平铺(repeated)、铺满(rounded)、拉伸(stretched)

##### 文本

* text-overflow
    - 当文本溢出包含元素时
    - clip 修剪元素
    - ellipsis 显示省略号来代表被修剪的文本
    - *string* 使用给定的字符串来显示被省略的文本
* text-shadow
    - 文本阴影
    - h-shadow 水平阴影的位置 允许负值
    - v-shadow 垂直阴影的位置 允许负值
    - blur 模糊的距离 可选
    - color 颜色
* text-wrap
    - 文本的换行规则
    - normal 只在允许的换行点进行换行
    - none 不换行 元素无法容纳的文本会溢出
    - unrestricted 在任意两个字符间换行
    - suppres 压缩元素中的换行。浏览器只在行中没有其他有效换行点时进行换行。
* word-break
    - 在恰当的断字点换行
    - normal 默认换行规则
    - break-all 允许在单词内换行
    - keep-all 只能在半角空格或连字符处换行
* word-wrap
    - 允许长单词或URL换行到下一行
    - normal
    - break-word 在长单词或 URL 地址内部进行换行。

##### 字体

```
@font-face
{
font-family: myFirstFont;   /*先定义字体名称*/
src: url('Sansation_Light.ttf'),    /*再引入字体文件*/
     url('Sansation_Light.eot'); /* IE9+ */
}

div{
    font-family:myFirstFont;    /*引用字体*/
}
```

若想使用粗体文本，需再添加另一个包含描述符的@font-face

```
@font-face
{
font-family: myFirstFont;   /*粗体字体名字跟上面正常的一样*/
src: url('Sansation_Bold.ttf'), /*另一个字体文件，包含了上面字体的粗体字符*/
     url('Sansation_Bold.eot'); /* IE9+ */
font-weight:bold;
}
```

##### 转换

###### 2D转换

Internet Explorer 10、Firefox 以及 Opera 支持 transform 属性。

* Chrome 和 Safari 需要前缀 -webkit- 
* IE9 需要 -ms-
* Opera 需要 -o-
* FireFox 需要 -mox-

**transform** :
* translate(xpx , ypx) //从左侧移动xpx 从顶端移动ypx
    - translateX(xpx)
    - translateY(ypx)  //只在一个轴上移动
* rotate(xdeg)         //顺时针旋转指定的角度(deg)
* scale(x , y)         //把元素的宽度转换为原始尺寸的x倍 把元素的高度转换为原始尺寸的y倍
    - scaleX(x)        
    - scaleY(y)        //只改变宽度或高度
* skew(xdeg , ydeg)          //围绕x轴把元素翻转x度 围绕y轴把元素翻转y度
    - skewX(x)         
    - skewY(y)         //只在一个轴上翻转

###### 3D转换

Internet Explorer 10 和 Firefox 支持 3D 转换。

Chrome和Safari需要前缀-webkit-

opera不支持

* rotateX(xdeg)         //围绕x轴以给定的度数进行旋转
* rotateY(ydeg)         //围绕y轴以给定的度数进行旋转

**transform-origin(20%,40%)** 
* 设置旋转元素的基点位置,x轴，y轴(如果是3D转换，再加一个z轴方向的值)
* 必须与tarnsform元素一起使用
* IE9 -ms- 仅适用于2D转换
* chrome/safari -webkit-
* opera只支持2D转换 

**transform-style** 
* 如何在3D空间内呈现被嵌套的元素
* flat 子元素不保留其3D位置
* preserve-3d 子元素保留其3D位置
* IE不支持
* -weblit-

##### 过渡

transtion,过渡是元素从一种样式逐渐改变为另一种的效果。

PS : 过渡效果通常在用户将鼠标指针浮动到元素上时发生。

必须规定两点内容：
* 把过渡效果添加到哪个属性上
* 效果的时长(时长如果没规定，则不会有过渡效果)

例：
```
div
{
transition: width 2s;
-moz-transition: width 2s;  /* Firefox 4 */
-webkit-transition: width 2s;   /* Safari 和 Chrome */
-o-transition: width 2s;    /* Opera */
}
```

如需向多个样式添加过渡效果，请添加多个属性，由逗号隔开

```
div
{
transition: width 2s, height 2s, transform 2s;
-moz-transition: width 2s, height 2s, -moz-transform 2s;
-webkit-transition: width 2s, height 2s, -webkit-transform 2s;
-o-transition: width 2s, height 2s,-o-transform 2s;
}
```

**transtion-property** 应用过渡效果的属性名称
* Internet Explorer 10、Firefox、Opera 和 Chrome 支持 transition-property 属性。
* Safari 支持替代的 -webkit-transition-property 属性。
* none 没有属性获得过渡效果
* all 所有属性获得过渡效果
* *property* 定义应用过渡效果的CSS属性名称列表，列表以逗号分隔

**transtion-duration** 过渡效果持续时间
* Internet Explorer 10、Firefox、Opera 和 Chrome 支持 transition-duration 属性。
* Safari 支持替代的 -webkit-transition-duration 属性。

**transtion-timing-function**  过渡效果的速度曲线
* Internet Explorer 10、Firefox、Opera 和 Chrome 支持 transition-timing-function 属性。
* Safari 支持替代的 -webkit-transition-timing-function 属性。
* linear 匀速
* ease 慢头快中慢尾
* ease-in 慢头
* ease-out 慢尾
* ease-in-out 慢头慢尾

**transtion-delay** 过渡效果开始前的等待
* Internet Explorer 10、Firefox、Opera 和 Chrome 支持 transition-delay 属性。
* Safari 支持替代的 -webkit-transition-delay 属性。

##### 动画

CSS3用 **@keyframes** 和 **animation** 实现

用 @keayframes 创建动画，用 animation 将动画绑定到选择器

animation
* 规定动画的名称
* 规定动画的时长

```
@keyframes myfirst
{
from {background: red;}/*from to 也可以改成0-100%*/
to {background: yellow;}
}
@-moz-keyframes myfirst /* Firefox */
{
from {background: red;}
to {background: yellow;}
}

@-webkit-keyframes myfirst /* Safari 和 Chrome */
{
from {background: red;}
to {background: yellow;}
}

@-o-keyframes myfirst /* Opera */
{
from {background: red;}
to {background: yellow;}
}

div
{
animation: myfirst 5s;
-moz-animation: myfirst 5s; /* Firefox */
-webkit-animation: myfirst 5s;  /* Safari 和 Chrome */
-o-animation: myfirst 5s;   /* Opera */
}
```

* animation-name 动画名称
* animation-duration 动画一次的周期 默认是0
* animation-timing-function 动画的速度曲线 默认ease
* animation-delay 动画延迟时间 默认是0
* animation-iteration-count 动画被播放次数 默认1
* animation-direction 规定动画是否方向轮流播
    - normal 默认值 动画正常播放
    - alternate 反向轮流播放
* animation-play-state 规定动画运行状态
    - 在JavaScript中使用该属性，就可以在播放过程中暂停动画
    - paused 动画已暂停
    - running 动画正在播放

##### 多列

* Internet Explorer 10 和 Opera 支持多列属性。
* Firefox 需要前缀 -moz-。
* Chrome 和 Safari 需要前缀 -webkit-。

* column-count 元素应该被分割的列数 
* column-gap 列与列之间的间隔
* column-rule 规定列之间的宽度、样式和颜色规则
    - column-rule-style 样式规则
        + none 
        + hidden
        + dotted 点状
        + dashed 虚线
        + solid 实线
        + double 双线
* column-span 规定元素应该横跨多少列
    - 1 横跨一列
    - all 横跨所有列
* column-width 列的宽度
* columhs 简写属性 列的宽度 和 列数

##### 用户界面

* appearance 
    - 所有主流浏览器都不支持 appearance 属性。
    - Firefox 支持替代的 -moz-appearance 属性。
    - Safari 和 Chrome 支持替代的 -webkit-appearance 属性。
    - normal 将元素呈现为常规元素
    - icon 呈现为图标
    - window 呈现为视口
    - button 呈现为按钮
    - menu 呈现为菜单
    - field 呈现为输入字段
* box-sizing 
    - content-box width与height只影响content 不涉及border和padding
    - border-box width与height影响边框盒，即border+padding+content
    - inherit
* outline-offset
    - 除了IE，主流浏览器都支持
    - 对轮廓进行偏移，并在边框边缘进行绘制
    - 轮廓与边框的区别：
        + 轮廓不占用空间
        + 轮廓可能是非矩形
    - *length* 轮廓到边缘的距离
    - inherit
* resize
    - Firefox 4+、Chrome 以及 Safari 不支持 resize。
    - 是否允许用户调整元素的尺寸
    PS : 如想此属性生效，需设置overflow属性，值可以是auto，hidden，scroll
    - none 用户无法调整尺寸
    - both 用户可调整宽高
    - horizontal 宽
    - vertical 高

[img1]: ../imgs/csszongjie.png "tututu"
[img2]: ../imgs/ct_boxmodel.gif "概述"