#### 本次主要研究波的行为
#### 模拟结果
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170108090243.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20170108090310.png)
#### 代码
```python
import numpy as np
import matplotlib.pyplot
from pylab import *
from math import *
import mpl_toolkits.mplot3d

dx=0.01
c=300.0 #speed
dt=dx/c
length=int(1.0/dx)
time=500
k=1000
y=[[0 for i in range(length)]for n in range(time)]#i represents x, n represents t
#initialize
#for i in range(length):
 #   y[0][i]=exp(-k*(i*dx-0.5-0.05)**2)
  #  y[1][i]=exp(-k*(i*dx-0.5-0.05)**2)
#for i in range(2*length/5):
 #   y[0][i]=3*i*dx
 #   y[1][i]=3*i*dx
for i in range(2*length/5,length):
    y[0][i]=2-2*i*dx
    y[1][i]=2-2*i*dx

#plot(range(length),y[1])
#show()

r=c*dt/dx
#iteration
for n in range(time-2):
    for i in range(1,length-1):
        y[n+2][i]=2*(1-r**2)*y[n+1][i]-y[n][i]+r**2*(y[n+1][i+1]+y[n+1][i-1])
y=array(y)
add=array([1 for i in range(length)])
for n in range(0,time,300):
    yp=y[n]+add*n/300
    plot(range(length),yp)
#xlim(-1,1)
xlabel('x')
#ylim(-1,1)
ylabel('y and t')
title('Waves on a string (fixed ends)')
#text(0,2,'reflection and inversion')#'$F_D$'
#savefig('wave 6.4.png')
#savefig('wave 6.2.png')
#savefig('wave .png')
figure(figsize=[16,8])
subplot(121)
y5=[]
t=array(range(time))*dt
for n in range(time):
    y5.append(y[n][4])
plot(t,y5)
xlabel('t/s')
ylabel('y/m')
title('vibration of a point on a string')
text(0,0.56,r'a point at 5% of this string')
subplot(122)
p=abs(np.fft.rfft(y5))**2
f = np.linspace(0, int(1/dt/2), len(p))
plot(f, p)
xlim(0,3000)
xlabel('Frequency(Hz)')
ylabel('Power')
title('Power spectrum')
#text(150,12000,'excited at center')
text(150,12000,'excited at 5% from its center')

#savefig('vibration 6.6 pluck.png')
savefig('vibration 6.6 fft 5.png')
#savefig('vibration .png')
show()

import matplotlib.pyplot as plt
import math
import numpy as np
from matplotlib import animation

delta_x, c ,r , k = 0.001, 300 , 1 , 1000
delta_t=delta_x/c
T=0.04
N=int(T*c/delta_x)
t=np.linspace(0,T,N+1)

def next_step(y_previous,y_current):
    y_next=[0]
    c1,c2=2*(1-r**2),r**2
    for i in range(1,len(y_current)-1):
        y_next.append(c1*y_current[i]-y_previous[i]+c2*(y_current[i-1]+y_current[i+1]))
    y_next.append(0)
    return y_next

def initial_Gaussian(x_excite):#initialize or excite the string in some point in the gaussian way
    y_initial=[]           
    for i in range(1+int(1./delta_x)):
        y_initial.append(math.exp(-k*(i*delta_x-x_excite)**2))
    return y_initial

def initial_real(x_excite):#initialize or excite the string in some point in the real way
    y_initial=[]
    for i in range(int(x_excite/delta_x)):
        y_initial.append(i*delta_x/x_excite)
    for i in range(int(x_excite/delta_x),1+int(1./delta_x)):
        y_initial.append((i*delta_x-1.)/(x_excite-1))
    return y_initial

def motion_of_a_point(x_observe,x_excite):
    y_initial=initial_real(x_excite) #this can be changed accrodingly
    y_observe=[]                  #calculate the displacement at x=0.05 or y(i=I,n)
    I=int(x_observe/delta_x)
    y0=y_initial
    y1=y_initial
    y_observe.append(y1[I])
    for i in range(N):
        y2=next_step(y0,y1)
        y0,y1=y1,y2
        y_observe.append(y1[I])
    return y_observe


#plot
x_observe_list,x_ex=[0.05,0.1,0.2,0.3],0.45


x_ob=x_observe_list[3]
yx=motion_of_a_point(x_ob,x_ex)
ps=abs(np.fft.rfft(yx))**2
freq= np.linspace(0, c/delta_x/2, len(ps))

plt.subplot(121)
plt.plot(t,yx)
plt.title('String Signal versus Time')
plt.xlabel('time(s)')
plt.ylabel('Signal(arbitrary units)')
#plt.text(0.,0.4,r'R Wavepacket,$y_0(x)=exp[-1000\times(x-%s)^2]$'%x_ex+'\n$x_{observe}=%s$'%x_ob)
plt.text(0,0.72,'Real Wavepacket of Two Straight Lines')
plt.xlim(0,T)

plt.subplot(1,2,2)
plt.plot(freq,ps)
plt.xlim(0,3000)
plt.xlabel('Frequency(Hz)')
plt.ylabel('Power')
plt.title('Power spectrum')
#plt.text(1500,200000,r'Gaussian Wavepacket'+'\n$y_0(x)=exp[-1000*(x-%s)^2]$'%x_ex+'\n$x_{observe}=%s$'%x_ob)
plt.text(1500,210000,r'Real Wavepacket'+'\n$x_{excite}=$%s'%x_ex+'\n$x_{observe}=%s$'%x_ob)


plt.show()
```

