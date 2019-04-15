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

#### 编写思路
1.初始化canvas的 dom结构 <br>

遇到的问题：

canvas.style.width/height 和 canvas.width/height 的区别？

简单来说  这两种方式设置的结果是不同的

通过style设置的宽高是canvas在浏览器中被渲染的宽高
通过canvas直接设置的是画布的直接宽高

2.创建初始圆心坐标对象，维护三个数组arr(存放初始圆心坐标对象) lastPoint(手指触摸过的圆心对象)  restPoint(剩余未触摸过的圆心对象) <br>
以初始化3 x 3个圆为例
半径的计算
