#### 此次我们研究的是电场和电势的问题
#### 公式推导如下
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/%E6%88%AA%E5%9B%BE20161211201607.png)
#### 首先考虑四方边界
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161211194325.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161211194359.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161211194410.png)
#### 再考虑由两个异号点电荷的情况
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161211195055.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161211195042.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161211195105.png)
#### 最后考虑三块带电平板的情况
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161211195804.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161211195732.png)
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161211195722.png)
##### 由以上的模拟，电势的变化规律确实符合沿电场线的方向减小
``` python
import numpy as np
from pylab import *
from math import *
import mpl_toolkits.mplot3d

V0=[[0 for i in range(21)]for j in range(21)]#i represents x, j represents y

for i in [6]:
    for j in range(6,15):
        V0[j][i]=1.0# j,i

for i in [14]:
    for j in range(6,14):
        V0[j][i]=1.0
for i in [10]:
    for j in range(6,14):
        V0[j][i]=1.0# j,i



#check
#for j in range(len(V0)):
#    for i in range(len(V0[1])):
#        print V0[i][j], 
#    print

VV=[]
VV.append(V0)

s=0
dx=0.1
#iteration
#for k in range(100):
while 1:
    VV.append(V0)
    for i in range(1,len(V0)-1):
        for j in range(1,len(V0[1])-1):
            VV[s+1][i][j]=(VV[s][i+1][j]+VV[s][i-1][j]+VV[s][i][j+1]+VV[s][i][j-1])/4.0
    for i in [6]:
        for j in range(6,14):
            VV[s+1][j][i]=1.0
    for i in [14]:
        for j in range(6,14):
            VV[s+1][j][i]=1.0
    for i in [10]:
        for j in range(6,14):
            VV[s+1][j][i]=1.0
       
    VV[s]=np.array(VV[s])
    VV[s+1]=np.array(VV[s+1])
    dVV=VV[s+1]-VV[s]
    dV=0
    for i in range(1,len(V0)-1):
        for j in range(1,len(V0[1])-1):
            dV=dV+abs(dVV[i][j])
    #print dV 
          
    s=s+1
    if dV<0.0001 and s>10:
        break
print s

V=array(VV[-1])
Ex=array(V0)
Ey=array(V0)
for j in range(1,len(V0)-1):
    for i in range(1,len(V0[1])-1):
        Ex[j][i]=-(V[j][i+1]-V[j][i-1])/(2*dx)
        Ey[j][i]=-(V[j+1][i]-V[j-1][i])/(2*dx)

#for i in range(len(V)):
#    for j in range(len(V[1])):
#        print V[i][j], 
#    print
figure(figsize=[8,8])
x=np.arange(-1.0,1.01,dx)#-1.0,-0.9,...,1.0
y=np.arange(-1.0,1.01,dx)
X,Y=np.meshgrid(x,y)
CS = contour(X,Y,V,15)
clabel(CS, inline=1, fontsize=10)
xlim(-1,1)
xlabel('x')
ylim(-1,1)
ylabel('y')
title('contours of electric potential')
savefig('electric potential J.png')
fig = figure()
ax = fig.add_subplot(111, projection='3d')
ax.plot_surface(X, Y, V,rstride=1, cstride=1,linewidth=0)
ax.set_xlabel('X')
ax.set_ylabel('Y')
ax.set_zlabel('V')
title('electric potential')
savefig('electric potential J 3D.png')
figure(figsize=[8,8])
Q=quiver(X,Y,Ex,Ey,scale=100)
xlim(-1,1)
xlabel('x')
ylim(-1,1)
ylabel('y')
title('electric field')
savefig('electric field J.png')
show()
```
#### 参考了郭潇学长的代码
