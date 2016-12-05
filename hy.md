#### 此次研究木星的小行星运动
##### 当改变小行星的初速度时
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161204205302.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161204205432.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161204205545.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161204205507.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161204205232.png)
##### 可以看出在v0=2pi时其运行才是稳定的
##### 当我们改变其离心率
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161204204148.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161204204059.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161204203856.png)
##### 当我们改变初始角度
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161204202444.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161204202304.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161204202232.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161204202139.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161204202027.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161204201901.png)
```python
import pylab as pl
import matplotlib.pyplot as plt
import math
class Hyperion :
    def __init__(self,theta=0,i=0,total_time=10, time_step=0.001, radius=1,e=0,a=1):
        self.x=[a*(1+e)]
        self.y=[0]
        self.vx=[0]
        self.vy=[3*math.pi]
        self.r=[radius]
        self.time=total_time
        self.dt=time_step
        self.beta=2
        self.alpha=0
        self.t=[0]
        self.theta=[theta]
        self.w=[0]
    def run(self):
        _time=0
        GM=4*(math.pi**2)
        r=1
        while(_time<self.time):
            self.r.append(math.sqrt(pow(self.x[-1],2)+pow(self.y[-1],2)))
            self.vx.append(self.vx[-1]-4*pow(math.pi,2)*(1+self.alpha/pow(self.r[-1],2))*self.x[-1]/pow(self.r[-1],1+self.beta)*self.dt)
            self.x.append(self.x[-1]+self.vx[-1]*self.dt)
            self.vy.append(self.vy[-1]-4*pow(math.pi,2)*(1+self.alpha/pow(self.r[-1],2))*self.y[-1]/pow(self.r[-1],1+self.beta)*self.dt)
            self.y.append(self.y[-1]+self.vy[-1]*self.dt)
            self.w.append(self.w[-1]-3*GM/(r**5)*(self.x[-1]*math.sin(self.theta[-1])-self.y[-1]*math.cos(self.theta[-1]))*\
                   (self.x[-1]*math.cos(self.theta[-1])+self.y[-1]*math.sin(self.theta[-1]))*self.dt)
            self.theta.append(self.dt*self.w[-1]+self.theta[-1])
            while self.theta[-1]>=1*math.pi:
                self.theta[-1]=self.theta[-1]-2*math.pi
            while  self.theta[-1]<=-1*math.pi:
                self.theta[-1]=self.theta[-1]+2*math.pi 
            self.t.append(_time)            
            _time += self.dt
    def show_results(self):
        pl.plot(self.t,self.theta)
        #pl.plot(self.t,self.w)
        #plt.plot(self.x,self.y)
        plt.ylabel('theta(radians)')
        #plt.ylabel('w(radians/yr)')
        plt.xlabel('time(yr)') 
        plt.legend()
        plt.title('Hyperion $\\theta$ versus time,v0=3pi')
        plt.show()
#Elliptical_Orbit_1 = Hyperion()
#Elliptical_Orbit_1.run()

#Elliptical_Orbit_2 = Hyperion(theta=1)
#Elliptical_Orbit_2.run()

#Delta_theta = []
#for n in range(len(Elliptical_Orbit_1.theta)):
    #Delta_theta.append(abs(Elliptical_Orbit_1.theta[n] - Elliptical_Orbit_2.theta[n]))

#pl.plot(Elliptical_Orbit_1.t, Delta_theta, "k")
#pl.yscale("log")
#plt.title('dtheta=1,e=0')

#pl.show()
Elliptical_Orbit = Hyperion()
Elliptical_Orbit.run()
Elliptical_Orbit.show_results()
```
#### 小行星的运动轨道要想稳定，条件很苛刻
#### 致谢由：于飞
