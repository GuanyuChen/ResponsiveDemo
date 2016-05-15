[TOC]

## Bootstrap学习笔记

## 全局样式

* `body`元素的`background-color`默认为`#ffffff`
* 为所有链接设置了基础颜色`@link-color`,并只有在`:hover`时才加下划线

## 布局容器

在最外层包裹

`.container`类适用于固定宽度并支持响应式布局的容器

    <div class='container'></div>

`.container-fluid`类适用于100%宽度，并占据全部视口(viewport)的容器

    <div class='container-fluid></div>

## 栅格系统

### 简介

栅格系统通过一系列行(row)和列(column)的组合来创建页面布局。

* row必须被`.container`或`.container-fluid`包裹起来
* 通过`row`在水平方向创建一组列`column`
* 内容放在列中，且只有列能直接作为`row`的子元素
* 如果一行中列的数目 > 12，多余的列将作为一个整体另起一行
* 通过为列设置`padding`属性来创建列与列之间的间隔。通过为`.row`设置负值的`margin`来抵消掉`.container`的`padding`，也就间接为列抵消掉了`padding`
* 栅格类应用于屏幕宽度大于或等于分界点的设备。

### 栅格参数

* 超小屏幕(<768px) `.col-xs-*` 水平排列
* 小屏幕(>=768px) `.col-sm-*` 开始时堆叠，大于阈值时水平排列
* 中等屏幕(>=992px) `.col-md-*` 同上
* 大屏幕(>=1200px) `.col-lg-*` 同上

### 列偏移

`.col-md-offset-*` 可以将列向右偏移相应的列。只管偏移，不管列的宽度。中间的规格参数可换成`sm` `xs` `lg`等其他的参数。

### 嵌套列

可以在列中再添加一个`.row`元素及其相应的列元素来构成列的嵌套。嵌套列一行也不能超过12(*其实没有要求一定要占满12列*)。

### 列排序

通过`.col-md-pull-*`和`.col-md-push-*`可以改变列的顺序， `pull`是拉到前面， `push`是推到后面。

