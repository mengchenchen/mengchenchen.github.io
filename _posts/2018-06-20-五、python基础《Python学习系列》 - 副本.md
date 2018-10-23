---
title: 《Python学习系列》4、python trutle绘图模块
tag: python
---

##### 简介



forward(d)  	向前移动d长度

backward(d)	向后移动d长度

right(d)		向右转动d度

left(d)		向左转动d度

goto(x,y)		移动到坐标（x,y）的位置

speed(speed)	笔画绘制的速度【0,10】



笔画控制命令

up()			笔画抬起

down()		笔画开启

setheadting(d)  箭头朝向d度

pensize(d)	笔画宽度	 	

pencolor(colorstr)	笔画颜色

reset()	重置所有设置，清空窗口

clear()	清空窗口，不会清空设置

circle(r,steps=e)	绘制一个圆形，r为半径，e为次数

begin_fill()	开始填充

fillcolor(colorstr)	填充颜色

end_fill()		结束填充



其他命令

done()	程序继续执行

undo()	车厢上一次动作

hideturtle()	隐藏箭头

showturtle()  显示箭头

screensize(x,y)



```python
# 导入turtle库
import turtle

turtle.forward(100)

turtle.done()
```



```python
# 元素元素的访问，索引从0开始，索引-1是最后一个
tuple = (1,2,3,4,5)
print(tuple[0])		# 1

# 修改
tuple[0]
```

