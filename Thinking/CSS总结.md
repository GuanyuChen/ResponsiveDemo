[TOC]

## CSS总结

### 本质

CSS本质可以分为宏观和微观两部分。宏观上它的存在就是为了控制页面的显示样式，包括布局，颜色，字体等。微观上则是实现这种控制功能的各种属性的定义和工作原理。

常用基础样式：

![常用基础样式][img1]

详细解释：

* 布局
    - float : 
        浮动的元素可以向左或向右移动，直到外边缘碰到包含元素或另一个浮动元素的边框为止。浮动的元素脱离文档流，文档流中其他元素忽视它。  
        浮动元素会生成一个块级框，无论它是什么元素，都会转成块级元素。需要宽度。  
        值：
        + right  向右浮动
        + left  向左浮动
        + none  默认值，不浮动。显示在文档流中的正常位置
        + inherit  从父元素继承float属性的值()
    - clear : 清除浮动
        值:
        + right : 清除右侧的浮动元素
        + left : 清除左侧的浮动元素
        + both : 清除左右两侧
        + none : 默认值，允许浮动元素出现在左右两侧
        + inherit : 从父元素继承(任何版本的IE都不支持inherit)
    PS : 当想让图片浮动到文本的左边，且 **图片和文本包含在另一个具有边框和背景的div中** 。有两种办法 :
    1. 把包含div(父div)也设置为浮动。但这样会使后面的元素受到影响。
    2. **在包含div中再添加一个空div，为这个div设置清除浮动**
    
    - display: 规定元素应该生成的框的类型
        值：
        + none : 此元素不会被显示
        + block : 显示为块级元素，前后都有换行符
        + inline : 显示为行内元素，前后没有换行符
        + inline-block : 行内块元素
        + inherit : 从父元素继承
    PS:display:none 与 visible:hidden 的区别:  
    display:none不为被隐藏的对象保留物理空间，“看不见也摸不到”  
    visible:hidden是对象在网页上不可见，但它的物理空间没有消失。

    - position:
        CSS有三种基本的定位机制：文档流，浮动，定位  
        文档流就是按照元素在文档中的顺序进行排列，块级元素从上到下排列，元素与元素之间的 **垂直距离由垂直外边距计算出来** 。行内元素在行中水平排列，可以使用 **水平内边距，边框和外边距** 调整它们的间距。但垂直内边距，边框和外边距 **不影响** 行内框的高度。
        **行框的高度总是足以容纳它包含的所有行内框。** 不过可以通过定义 **行高(line-height)** 来改变行框的高度。
        值：
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
    - width: 
    - height:
    - padding: 
    - margin:
    - border:
* 颜色、背景
    - color: 
    - background: 
        + -color:
        + -image:
        + -repeat:
        + -position:
        + -attachment:
        + -size:
        + -clip:
        + -origin:
* 字体
    - -family:
    - -weight:
    - -size:
    - -style:
    - -variant:
    - -stretch:
* 文本
    - text-index:
    - text-align:
    - line-height:
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
    - word-spacing:
    - letter-spacing:
    - text-transform:
    - text-decoration:
    - text-shadow:
    - white-space:
    - direction:



[img1]: ../imgs/csszongjie.png "tututu"