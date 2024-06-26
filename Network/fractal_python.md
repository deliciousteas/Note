
> 用python的turtle库做了两个分形树的测试，测试turtle画图效果，其中了解了python中return可以不追加任何参数默认返回None的情况。
return在函数结束前，返回1-N个值。可以任何数据类型，甚至其他函数。

一种特殊情况:不指定返回值，默认返回`None`。满足这个条件提前结束函数执行函数执行，将控制权返回给**调用函数(caller)**。

 ` if i<10:        ` 

`return`

在用turtle画图时，return意味着不再递归调用自身，结束执行返回到调用函数处。
## 结果图如下：
![4fe41a44046d65b1781e0d874bb5a68](https://github.com/deliciousteas/Note/assets/107855849/5f6b5743-3430-4a72-8d17-420c4f38b94c)

![a847aed9737b3b055d89d8a94382d1c](https://github.com/deliciousteas/Note/assets/107855849/f1c67b8a-87e2-42ea-a9df-f60380d386ed)

![a863e8869271422edbd781fc69f000e](https://github.com/deliciousteas/Note/assets/107855849/427da60d-b243-4a65-ab46-4e572445b817)

## demo1如下：
import turtle
#创建一个canvas画板
hr=turtle.Turtle()

#设置canvas初始箭头角度
#turtle默认是向右的，水平方向
hr.left(90)

#设置canvas画图速度，可以输入参数：fastest,fast,normal,slow,slowest或者数0-10的数字
hr.speed(0)

hr.penup()
hr.goto(20,-300)
hr.pendown()
def baba(xdummy, ydummy):
    turtle.clearscreen()
    turtle.bye()
def tree(i):
    if i<10:
        return #符合条件，不再绘制树，返回调用函数处。
    else:
        #向前移动i个单位
        hr.forward(i)
        #向左旋转30度
        hr.left(30)
        tree(3*i/4)
        hr.right(60)
        tree(3*i/4)
        hr.left(30)
        hr.backward(i)
tree(120)

turtle.done()
hr.write("  Click me!", font=("Courier", 12, "bold"))
hr.onclick(baba, 1)

## demo2如下：

import random
import turtle
from turtle import *


def grow(length, decrease, angle, noise=0):
    if length > 10:

        turtle.width(length / 10)
        turtle.forward(length)
        new_length = length * decrease
        if noise > 0:
            new_length *= random.uniform(0.9, 1.1)

        angle_l = angle
        angle_r = angle

        turtle.left(angle_l)
        grow(new_length, decrease, angle, noise)
        turtle.right(angle_l)

        turtle.right(angle_r)
        grow(new_length, decrease, angle, noise)
        turtle.left(angle_r)

        turtle.backward(length)
    return

turtle.penup()
turtle.goto(0, -300)
turtle.pendown()
turtle.left(90)
turtle.speed(0)
grow(150, 0.8, 23.3,10 )
turtle.done()

# 参考
[demo2教程](https://www.youtube.com/watch?v=EICpm9rnPjE)
[demo1教程](https://www.youtube.com/watch?v=RWtNQ8RQkO8)
