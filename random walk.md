#### 一、摘要
###### 本次是用计算机来模拟随机过程，此次研究的主要内容是随机行走，即让质点在一个空间里向各个方向随机的移动，观察其最后的位置离远点的距离随时间变化的关系
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/3874109ca75a96966ea9c0e479455003.jpg)
#### 二、作业内容
##### 1.一维随机行走
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170107202132.png)
##### 2.三维随机行走
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170107202132.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170107202225.png)
###### 以下三维随机的模拟结果
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170107202933.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170107203031.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170107203113.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170107203201.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170107203250.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170107203328.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170107203428.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170107203505.png)
##### 3.三维saw过程
###### saw的模拟结果)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170107203735.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170107203822.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170107203901.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170107203932.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170107204012.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170107204038.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170107204118.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170107204200.png)
#### 三、代码
##### 1、三维随机
```python
import pylab as pl
import math
import random
import numpy as np
from matplotlib import animation
class rwalk:
    def __init__(self,r=0,r2a=0,x=0,y=0,z=0,dt=1):
        self.x=[0]
        self.y=[0]
        self.z=[0]
        self.r=[0]
        #self.vy=[math.sqrt(4*math.pi*math.pi/pow(r,beita-1))]
        self.r2a=[0]
        self.x2a=[0]
        self.y2a=[0]
        self.z2a=[0]
        
        self.dt=dt
        
        self.t=[1]
        
    def caculate(self):
        for i in range(0,1000):
            theta=math.pi*random.uniform(0, 1)  
            fi=2*math.pi*random.uniform(0, 1)
            self.x.append(self.x[i]+math.sin(theta)*math.cos(fi))
            self.y.append(self.y[i]+math.sin(theta)*math.sin(fi))
            self.z.append(self.x[i]+math.cos(theta))
            self.x2a.append((self.x2a[i]+math.sin(theta)*math.cos(fi)*math.sin(theta)*math.cos(fi)))
            self.y2a.append((self.y2a[i]+math.sin(theta)*math.sin(fi)*math.sin(theta)*math.sin(fi)))
            self.z2a.append((self.z2a[i]+math.cos(theta)*math.cos(theta))) 
            self.r.append(pow(self.x[i]*self.x[i]+self.y[i]*self.y[i]+self.z[i]*self.z[i],0.5))
            self.r2a.append(self.x2a[i]+self.y2a[i]+self.z2a[i])
            self.t.append(self.t[i]+self.dt)            
    def show(self):
        
        pl.plot(self.t,self.r2a,"b")
        pl.xlabel('t')
        pl.ylabel('r2a')
        pl.show()



p=rwalk()
p.caculate()
p.show()
```
##### 2.saw问题代码
```python
from __future__ import division
import pylab as pl
import math
import random
import numpy as np
from matplotlib import animation

class rwalk:
    def __init__(self,r=0,r2a=0,x=0,y=0,z=0,dt=1.0):
        self.x=[0]
        self.y=[0]
        self.z=[0]
        self.r=[0]
        #self.vy=[math.sqrt(4*math.pi*math.pi/pow(r,beita-1))]
        self.r2a=[0]
        self.x2a=[0]
        self.y2a=[0]
        self.z2a=[0]
        
        self.dt=dt
        
        self.t=[0]
        self.p1=0
        self.p2=0
        self.p3=0
        self.p4=0
        self.p5=0
        self.p6=0
    def caculate(self):
        for i in range(0,100):
            if "self.x[-1]+1"in self.x:
                self.p1=0
            else:
                self.p1=1/6.0
            if "self.x[-1]-1"in self.x:
                self.p2=0
            else:
                self.p2=1/6.0
            if "self.y[-1]+1"in self.y:
                self.p3=0
            else:
                self.p3=1/6.0
            if "self.y[-1]-1"in self.y:
                self.p4=0
            else:
                self.p4=1/6.0
            if "self.z[-1]+1"in self.z:
                self.p5=0
            else:
                self.p5=1/6.0
            if "self.z[-1]-1"in self.z:
                self.p6=0
            else:
                self.p6=1/6.0

            self.p1=self.p1/(self.p1+self.p2+self.p3+self.p4+self.p5+self.p6)
            self.p2=(self.p1+self.p2)/(self.p1+self.p2+self.p3+self.p4+self.p5+self.p6)
            self.p3=(self.p1+self.p2+self.p3)/(self.p1+self.p2+self.p3+self.p4+self.p5+self.p6)
            self.p4=(self.p1+self.p2+self.p3+self.p4)/(self.p1+self.p2+self.p3+self.p4+self.p5+self.p6)
            self.p5=(self.p1+self.p2+self.p3+self.p4+self.p5)/(self.p1+self.p2+self.p3+self.p4+self.p5+self.p6)
            self.p6=(self.p1+self.p2+self.p3+self.p4+self.p5+self.p6)/(self.p1+self.p2+self.p3+self.p4+self.p5+self.p6)
            u=random.uniform(0, 1)

            if (0<=u<self.p1):
                a=self.x[-1]+1.0
                b=self.y[-1]
                c=self.z[-1]
                self.x.append(a)
                self.y.append(b)
                self.z.append(c)
                d=self.x2a[-1]+1.0
                e=self.y2a[-1]
                f=self.z2a[-1]
                self.x2a.append(d)
                self.y2a.append(e)
                self.z2a.append(f)
                g=self.x2a[-1]+self.y2a[-1]+self.z2a[-1]
                self.r2a.append(g)
                h=self.t[-1]+self.dt
                self.t.append(h)
                self.r.append(pow(self.x[i]*self.x[i]+self.y[i]*self.y[i]+self.z[i]*self.z[i],0.5))
            elif (self.p1<=u<self.p2):
                a=self.x[-1]-1.0
                b=self.y[-1]
                c=self.z[-1]
                self.x.append(a)
                self.y.append(b)
                self.z.append(c)
                d=self.x2a[-1]+1.0
                e=self.y2a[-1]
                f=self.z2a[-1]
                self.x2a.append(d)
                self.y2a.append(e)
                self.z2a.append(f)
                g=self.x2a[-1]+self.y2a[-1]+self.z2a[-1]
                self.r2a.append(g)
                h=self.t[-1]+self.dt
                self.t.append(h)
                self.r.append(pow(self.x[i]*self.x[i]+self.y[i]*self.y[i]+self.z[i]*self.z[i],0.5))
            elif (self.p2<=u<self.p3):
                a=self.x[-1]
                b=self.y[-1]+1.0
                c=self.z[-1]
                self.x.append(a)
                self.y.append(b)
                self.z.append(c)
                d=self.x2a[-1]
                e=self.y2a[-1]+1.0
                f=self.z2a[-1]
                self.x2a.append(d)
                self.y2a.append(e)
                self.z2a.append(f)
                g=self.x2a[-1]+self.y2a[-1]+self.z2a[-1]
                self.r2a.append(g)
                h=self.t[-1]+self.dt
                self.t.append(h)
                self.r.append(pow(self.x[i]*self.x[i]+self.y[i]*self.y[i]+self.z[i]*self.z[i],0.5))
            elif (self.p3<=u<self.p4):
                a=self.x[-1]
                b=self.y[-1]-1.0
                c=self.z[-1]
                self.x.append(a)
                self.y.append(b)
                self.z.append(c)
                d=self.x2a[-1]
                e=self.y2a[-1]+1.0
                f=self.z2a[-1]
                self.x2a.append(d)
                self.y2a.append(e)
                self.z2a.append(f)
                g=self.x2a[-1]+self.y2a[-1]+self.z2a[-1]
                self.r2a.append(g)
                h=self.t[-1]+self.dt
                self.t.append(h)
                self.r.append(pow(self.x[i]*self.x[i]+self.y[i]*self.y[i]+self.z[i]*self.z[i],0.5))
            elif (self.p4<=u<self.p5):
                a=self.x[-1]
                b=self.y[-1]
                c=self.z[-1]+1.0
                self.x.append(a)
                self.y.append(b)
                self.z.append(c)
                d=self.x2a[-1]
                e=self.y2a[-1]
                f=self.z2a[-1]+1.0
                self.x2a.append(d)
                self.y2a.append(e)
                self.z2a.append(f)
                g=self.x2a[-1]+self.y2a[-1]+self.z2a[-1]
                self.r2a.append(g)
                h=self.t[-1]+self.dt
                self.t.append(h)
                self.r.append(pow(self.x[i]*self.x[i]+self.y[i]*self.y[i]+self.z[i]*self.z[i],0.5))
            elif (self.p5<=u<=self.p6):
                a=self.x[-1]
                b=self.y[-1]
                c=self.z[-1]-1.0
                self.x.append(a)
                self.y.append(b)
                self.z.append(c)
                d=self.x2a[-1]
                e=self.y2a[-1]
                f=self.z2a[-1]+1.0
                self.x2a.append(d)
                self.y2a.append(e)
                self.z2a.append(f)
                g=self.x2a[-1]+self.y2a[-1]+self.z2a[-1]
                self.r2a.append(g)
                h=self.t[-1]+self.dt
                self.t.append(h)
                self.r.append(pow(self.x[i]*self.x[i]+self.y[i]*self.y[i]+self.z[i]*self.z[i],0.5))
           
    def show(self):
        pl.plot(self.t,self.r,"b")
        pl.xlabel('t')
        pl.ylabel('r')
        pl.show()

q=rwalk()
q.caculate()
q.show()
```
#### 四、实验结论
1.对于随机行走，粒子的最终位置的方均值无论是完全自由的三维随机还是saw随机都随步数 N（时间）增大而增大，且saw过程增大的更快一点
2.对于完全自由的随机行走，粒子最可能出现的位置是原点

#### 五、实验反思
在我的模拟中似乎saw问题由完全自由的随机行走粒子最终位置的方均值差距好像不太大，但是经分析，saw的应该更大一些，猜测应该是在计算<r^2>时出现了问题(但是没有找到)
