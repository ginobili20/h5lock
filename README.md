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
canvas.style.width/height 和 canvas.width/height 的区别？ <br>
简单来说  这两种方式设置的结果是不同的 <br>
通过style设置的宽高是canvas在浏览器中被渲染的宽高 <br>
通过canvas直接设置的是画布的直接宽高 <br>

2.创建初始圆心坐标对象，维护三个数组arr(存放初始圆心坐标对象) lastPoint(手指触摸过的圆心对象)  restPoint(剩余未触摸过的圆心对象) <br>
以初始化3 x 3个圆为例半径的计算
![半径](https://github.com/ginobili20/h5lock/raw/master/img/r.png) <br>
```
this.r = this.ctx.canvas.width / (4 * n + 2)
```
圆心坐标的计算
```
x: 3 * r + 4 * j * r,
y: 3 * r + 4 * i * r,
```

3.得到基础圆心坐标 遍历arr绘制圆 <br>
使用canvas的绘圆方法 ctx.arc(x, y, r, startDeg, endDeg) <br>

4.绑定touch事件 <br>
touchstart <br>
需要判断触摸的位置是否在初始圆心内 <br>
首先计算 触摸点到画布的坐标  = 触摸点到屏幕的距离 - 画布到屏幕的距离 <br>
再遍历的判断是否在初始圆内 触摸点的坐标 - 圆心坐标 是否  小于 半径 <br>
如果在圆内 则在这个圆内 添加一个实心圆 代表触摸过的圆 将坐标对象push进入lastPoint数组，从restPoint中删除这个坐标 同时将touchFlag置为true <br>

touchmove <br>
移动的时候更新画布内容 每次更新的时候需要先清空画布 然后重画基础圆，以及已经触摸过的圆和途径的线条<br>
判断移动的时候是否移动到了restPoint中的圆内（之前没有触摸过的圆） <br>
如果是 那么 画实心圆以及线段 <br>

touchend <br>
讲touchFlag置为false 300ms后重置画布 （重新创建圆坐标，绘制基础圆）<br>
存储密码 <br>
维护一个pswObj对象<br>
pswObj.step为undefined的时候为用户第一次绘制 pswObj.fpassword保存第一次绘制的图案 然后将step置为1 标题提示用户再次绘制 <br>
pswObj.step为1的时候 表示用户再次绘制 判断两次的密码是否相同 相同则显示绿色框 并且pswObj.spassword保存密码 step置为2 <br>

```localStorage.setItem（'passwordxx', JSON.stringify(pswObj.spassword)）```

不同则删除step 标题显示 两次输入密码不一致 显示红色框 <br>
pswObj.step为2的时候，表示已经存储了密码，用户绘制的时候 判断是否与存储的密码一致 一致则解锁成功，否则失败 <br>

5.rest的时候控制右上角重置密码字样的显隐状态 <br>
只有当step为2的时候显示重置密码 其余时候隐藏<br>
为重置密码绑定点击事件 点击清除localStorage中保存的密码<br>

6.初始化<br>
初始化阶段 获取localStorage中的密码存入pswObj中
初始化阶段 获取localStorage中的密码存入pswObj中






