####  粒子的衰变问题
##### 对过程的分析以及解决方法![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161009213933.png)
##### 用欧勒法的模拟效果和对程序的检验及运行截图![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161009205843.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161009205917.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161009205935.png)
##### 程序源代码
``` python
import pylab as pl
class uranium_decay:
    """
    Simulation of radioactive decay
    Program to accompany 'Computational Physics' by Cai Hao
    """
    def __init__(self, number_of_nucleiA = 100,number_of_nucleiB = 0, time_constant = 1, time_of_duration = 5, time_step = 0.01):
        # unit of time is second
        self.NA = [number_of_nucleiA]
        self.NB = [number_of_nucleiB]
        self.t = [0]
        self.tau = time_constant
        self.dt = time_step
        self.time = time_of_duration
        self.nsteps = int(time_of_duration // time_step + 1)
        print("Initial number of NA ->", number_of_nucleiA)
        print("Initial number of NA ->", number_of_nucleiB)
        print("Time constant ->", time_constant)
        print("time step -> ", time_step)
        print("total time -> ", time_of_duration)
    def calculate(self):
        for i in range(self.nsteps):
            tmp1 = self.NA[i] + (self. NB[i]-self.NA[i]) / self.tau * self.dt
            tmp2 = self.NB[i] + (self. NA[i]-self.NB[i]) / self.tau * self.dt                         
            self.NA.append(tmp1)
            self.NB.append(tmp2)                          
            self.t.append(self.t[i] + self.dt)
    def show_results(self):
        plot1, = pl.plot(self.t, self.NA,'b')
        plot2, = pl.plot(self.t, self.NB,'g')
        pl.title('Nuclei Decay')
        pl.xlabel('time ($s$)')
        pl.ylabel('Number of Nuclei')
        first_legend=pl.legend([plot1, plot2], ['Particle A', 'Particle B'], loc="best")
        pl.show()
    def store_results(self):
        myfile = open('nuclei_decay_data.txt', 'w')
        for i in range(len(self.t)):
            print(self.t[i], self.n_uranium[i], file = myfile)
        myfile.close()

a = uranium_decay()
a.calculate()
a.show_results()

from math import *
class exact_results_check(uranium_decay):
    def show_results(self):
        self.etNA = []
        self.etNB = []
        for i in range(len(self.t)):
            tempA = 0.5*((self.NA[0]-self.NB[0])*exp(-2*self.t[i])+(self.NA[0]+self.NB[0]))
            tempB = 0.5*((self.NB[0]-self.NA[0])*exp(-2*self.t[i])+(self.NA[0]+self.NB[0]))
            self.etNA.append(tempA)
            self.etNB.append(tempB)
        pl.plot(self.t, self.etNA)
        pl.plot(self.t, self.etNB)
        pl.plot(self.t, self.NA, '*')
        pl.plot(self.t, self.NB, '+')
        pl.xlabel('time ($s$)')
        pl.ylabel('Number of Nuclei')
        pl.xlim(0, self.time)
        pl.show()
b = exact_results_check(number_of_nucleiA=100,number_of_nucleiB=0, time_constant=1, time_step=0.05)
b.calculate()
b.show_results()


class diff_step_check(uranium_decay):
    def show_results(self, style = 'b'):
        pl.plot(self.t, self.NA, 'r')
        pl.plot(self.t, self.NB, 'g')
        pl.xlabel('time ($s$)')
        pl.ylabel('Number of Nuclei')
        pl.xlim(0, self.time)
from pylab import *
b = diff_step_check(number_of_nucleiA=100,number_of_nucleiB=0, time_constant=1, time_step=0.01)
b.calculate()
b.show_results()
c = diff_step_check(number_of_nucleiA=95,number_of_nucleiB=5, time_constant=1, time_step=0.02)
c.calculate()
c.show_results('r')
show()
``` 
##### 讨论与分析
###### 在写代码是要注意将constant-t保持一样，否则将导致图像的比例不一样
##### 致谢：感谢百度帮我安装matplotlip,感谢于飞同学帮我挑出错误
