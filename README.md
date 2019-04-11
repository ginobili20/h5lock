# h5lock 移动端绘制解锁图案功能

--------

### 概述
请使用移动端体验 
[戳我](https://ginobili20.github.io/h5lock/)

####  主要技术栈
> 
* [x] canvas
* [x] localStorage


#### 主要功能
1.保存设置的解锁图案<br>
2.判断解锁图案正确与否

#### 编写流程
1.初始化canvas的 dom结构 <br>

遇到的问题：
```
canvas.style.width/height 和 canvas.width/height 的区别
在w3网站上是这样解释的：
The canvas element has two attributes to control the size of the coordinate space: width and height.
These attributes, when specified, must have values that are valid non-negative integers. 
The rules for parsing non-negative integers must be used to obtain their numeric values. If an attribute is missing,
or if parsing its value returns an error, then the default value must be used instead. The width attribute defaults to 300,
and the height attribute defaults to 150.

The intrinsic dimensions of the canvas element equal the size of the coordinate space, with the numbers interpreted in CSS pixels. 
However, the element can be sized arbitrarily by a style sheet. During rendering, the image is scaled to fit this layout size.

简单来说  这两种方式设置的结果是不同的

通过style设置的宽高是canvas在浏览器中被渲染的宽高
通过canvas直接设置的是画布的直接宽高
```

