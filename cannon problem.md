### 加农炮射程问题
#### 问题的分析如下：为无风阻和有风阻两种情况
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161017071547.png)
##### 在无风阻时的运行效果截图
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161017070048.png)
##### 有风阻时和无风阻时对比的运行效果截图
![github](https://github.com/Huangyu007/compuational_physics_N2014301020030/blob/master/QQ%E6%88%AA%E5%9B%BE20161017072218.png)
#### 程序源代码
```python
import pylab as pl
import math
class cannon:
    def __init__(self,  initial_x=0,initial_y=0, time_step=0.1, initial_velocity=700,initial_ag=math.pi/180,g=9.8):
        self.dt = time_step
        self.x_45=[initial_x]
        self.y_45=[initial_y]  
        self.Vx_45= [initial_velocity*math.cos(45*initial_ag)]
        self.Vy_45= [initial_velocity*math.sin(45*initial_ag)]
        self.x_15=[initial_x]
        self.y_15=[initial_y]  
        self.Vx_15= [initial_velocity*math.cos(15*initial_ag)]
        self.Vy_15= [initial_velocity*math.sin(15*initial_ag)]
        self.x_75=[initial_x]
        self.y_75=[initial_y]  
        self.Vx_75= [initial_velocity*math.cos(75*initial_ag)]
        self.Vy_75= [initial_velocity*math.sin(75*initial_ag)]
        self.g = g
    def calculate(self):
        while(1):
            tmp1_45 = self.Vx_45[-1] 
            tmp2_45 = self.Vy_45[-1] -self.g* self.dt
            tmp3_45 = self.x_45[-1] + self.Vx_45[-1]* self.dt
            tmp4_45 = self.y_45[-1] + self.Vy_45[-1]* self.dt
            self.Vx_45.append(tmp1_45)
            self.Vy_45.append(tmp2_45)
            self.x_45.append(tmp3_45)
            self.y_45.append(tmp4_45)
            if (tmp4_45<0):
                break
        x1_45 = self.x_45[-2]
        y1_45 = self.x_45[-2]
        x2_45 = self.y_45[-1]
        y2_45 = self.y_45[-1]    
        temp_45 = x1_45 - (y1_45) * ((x2_45 - x1_45)/(y2_45 - y1_45))
        self.x_45[-1] = temp_45
        self.y_45[-1] =          0
        
        while(1):
            tmp1_15 = self.Vx_15[-1] 
            tmp2_15 = self.Vy_15[-1] -self.g* self.dt
            tmp3_15 = self.x_15[-1] + self.Vx_15[-1]* self.dt
            tmp4_15 = self.y_15[-1] + self.Vy_15[-1]* self.dt
            self.Vx_15.append(tmp1_15)
            self.Vy_15.append(tmp2_15)
            self.x_15.append(tmp3_15)
            self.y_15.append(tmp4_15)
            if (tmp4_15<0):
                break
        x1_15 = self.x_15[-2]
        y1_15 = self.x_15[-2]
        x2_15 = self.y_15[-1]
        y2_15 = self.y_15[-1]    
        temp_15 = x1_15 - (y1_15) * ((x2_15 - x1_15)/(y2_15 - y1_15))
        self.x_15[-1] = temp_15
        self.y_15[-1] =          0

        while(1):
            tmp1_75 = self.Vx_75[-1] 
            tmp2_75 = self.Vy_75[-1] -self.g* self.dt
            tmp3_75 = self.x_75[-1] + self.Vx_75[-1]* self.dt
            tmp4_75 = self.y_75[-1] + self.Vy_75[-1]* self.dt
            self.Vx_75.append(tmp1_75)
            self.Vy_75.append(tmp2_75)
            self.x_75.append(tmp3_75)
            self.y_75.append(tmp4_75)
            if (tmp4_75<0):
                break
        x1_75 = self.x_75[-2]
        y1_75 = self.x_75[-2]
        x2_75 = self.y_75[-1]
        y2_75 = self.y_75[-1]    
        temp_75 = x1_75 - (y1_75) * ((x2_75 - x1_75)/(y2_75 - y1_75))
        self.x_75[-1] = temp_75
        self.y_75[-1] =          0
        
                    
    def show_results(self):
        plot1,=pl.plot(self.x_45, self.y_45,'r')
        plot2,=pl.plot(self.x_15, self.y_15,'g')
        plot3,=pl.plot(self.x_75, self.y_75,'b')
        pl.title('cannon without air resistance')
        first_legend=pl.legend([plot1, plot2,plot3], ['45', '15','75'], loc="best") 
        pl.show()
        
a = cannon()
a.calculate()
a.show_results()

import pylab as pl
import math
class cannon:
    def __init__(self,  initial_x=0,initial_y=0, time_step=0.1, initial_velocity=700,initial_ag=math.pi/180,g=9.8):
        self.dt = time_step
        self.x_45=[initial_x]
        self.y_45=[initial_y]  
        self.Vx_45= [initial_velocity*math.cos(45*initial_ag)]
        self.Vy_45= [initial_velocity*math.sin(45*initial_ag)]
        self.x_15=[initial_x]
        self.y_15=[initial_y]  
        self.Vx_15= [initial_velocity*math.cos(15*initial_ag)]
        self.Vy_15= [initial_velocity*math.sin(15*initial_ag)]
        self.x_75=[initial_x]
        self.y_75=[initial_y]  
        self.Vx_75= [initial_velocity*math.cos(75*initial_ag)]
        self.Vy_75= [initial_velocity*math.sin(75*initial_ag)]
        self.air_x_45=[initial_x]
        self.air_y_45=[initial_y]  
        self.air_Vx_45= [initial_velocity*math.cos(45*initial_ag)]
        self.air_Vy_45= [initial_velocity*math.sin(45*initial_ag)]
        self.air_x_15=[initial_x]
        self.air_y_15=[initial_y]  
        self.air_Vx_15= [initial_velocity*math.cos(15*initial_ag)]
        self.air_Vy_15= [initial_velocity*math.sin(15*initial_ag)]
        self.air_x_75=[initial_x]
        self.air_y_75=[initial_y]  
        self.air_Vx_75= [initial_velocity*math.cos(75*initial_ag)]
        self.air_Vy_75= [initial_velocity*math.sin(75*initial_ag)]
        self.g = g
    def calculate(self):
        while(1):
            tmp1_45 = self.Vx_45[-1] 
            tmp2_45 = self.Vy_45[-1] -self.g* self.dt
            tmp3_45 = self.x_45[-1] + self.Vx_45[-1]* self.dt
            tmp4_45 = self.y_45[-1] + self.Vy_45[-1]* self.dt
            self.Vx_45.append(tmp1_45)
            self.Vy_45.append(tmp2_45)
            self.x_45.append(tmp3_45)
            self.y_45.append(tmp4_45)
            if (tmp4_45<0):
                break
        x1_45 = self.x_45[-2]
        y1_45 = self.x_45[-2]
        x2_45 = self.y_45[-1]
        y2_45 = self.y_45[-1]    
        temp_45 = x1_45 - (y1_45) * ((x2_45 - x1_45)/(y2_45 - y1_45))
        self.x_45[-1] = temp_45
        self.y_45[-1] =          0
       
        while(1):
            air_tmp1_45 =self.air_Vx_45[-1] -0.00004*700*self.air_Vx_45[-1]*self.dt
            air_tmp2_45 =self.air_Vy_45[-1] -self.g* self.dt-0.00004*700*self.air_Vy_45[-1]*self.dt
            air_tmp3_45 = self.air_x_45[-1] + self.air_Vx_45[-1]* self.dt
            air_tmp4_45 = self.air_y_45[-1] + self.air_Vy_45[-1]* self.dt
            self.air_Vx_45.append(air_tmp1_45)
            self.air_Vy_45.append(air_tmp2_45)
            self.air_x_45.append(air_tmp3_45)
            self.air_y_45.append(air_tmp4_45)
            if (air_tmp4_45<0):
                break
        air_x1_45 = self.air_x_45[-2]
        air_y1_45 = self.air_x_45[-2]
        air_x2_45 = self.air_y_45[-1]
        air_y2_45 = self.air_y_45[-1]    
        air_temp_45 = air_x1_45 - (air_y1_45) * ((air_x2_45 - air_x1_45)/(air_y2_45 - air_y1_45))
        self.air_x_45[-1] = air_temp_45
        self.air_y_45[-1] =          0
       
        while(1):
            tmp1_15 = self.Vx_15[-1] 
            tmp2_15 = self.Vy_15[-1] -self.g* self.dt
            tmp3_15 = self.x_15[-1] + self.Vx_15[-1]* self.dt
            tmp4_15 = self.y_15[-1] + self.Vy_15[-1]* self.dt
            self.Vx_15.append(tmp1_15)
            self.Vy_15.append(tmp2_15)
            self.x_15.append(tmp3_15)
            self.y_15.append(tmp4_15)
            if (tmp4_15<0):
                break
        x1_15 = self.x_15[-2]
        y1_15 = self.x_15[-2]
        x2_15 = self.y_15[-1]
        y2_15 = self.y_15[-1]    
        temp_15 = x1_15 - (y1_15) * ((x2_15 - x1_15)/(y2_15 - y1_15))
        self.x_15[-1] = temp_15
        self.y_15[-1] =          0
       
        while(1):
            air_tmp1_15 = self.air_Vx_15[-1] -0.00004*700*self.air_Vx_15[-1]*self.dt
            air_tmp2_15 = self.air_Vy_15[-1] -self.g* self.dt-0.00004*700*self.air_Vy_15[-1]*self.dt
            air_tmp3_15 = self.air_x_15[-1] +self.air_Vx_15[-1]* self.dt
            air_tmp4_15 = self.air_y_15[-1] + self.air_Vy_15[-1]* self.dt
            self.air_Vx_15.append(air_tmp1_15)
            self.air_Vy_15.append(air_tmp2_15)
            self.air_x_15.append(air_tmp3_15)
            self.air_y_15.append(air_tmp4_15)
            if (air_tmp4_15<0):
                break
        air_x1_15 = self.air_x_15[-2]
        air_y1_15 = self.air_x_15[-2]
        air_x2_15 = self.air_y_15[-1]
        air_y2_15 = self.air_y_15[-1]    
        air_temp_15 = air_x1_15 - (air_y1_15) * ((air_x2_15 - air_x1_15)/(air_y2_15 - air_y1_15))
        self.air_x_15[-1] = air_temp_15
        self.air_y_15[-1] =          0
        
        while(1):
            tmp1_75 = self.Vx_75[-1] 
            tmp2_75 = self.Vy_75[-1] -self.g* self.dt
            tmp3_75 = self.x_75[-1] + self.Vx_75[-1]* self.dt
            tmp4_75 = self.y_75[-1] + self.Vy_75[-1]* self.dt
            self.Vx_75.append(tmp1_75)
            self.Vy_75.append(tmp2_75)
            self.x_75.append(tmp3_75)
            self.y_75.append(tmp4_75)
            if (tmp4_75<0):
                break
        x1_75 = self.x_75[-2]
        y1_75 = self.x_75[-2]
        x2_75 = self.y_75[-1]
        y2_75 = self.y_75[-1]    
        temp_75 = x1_75 - (y1_75) * ((x2_75 - x1_45)/(y2_75 - y1_75))
        self.x_75[-1] = temp_75
        self.y_75[-1] =          0
       
        while(1):
            air_tmp1_75 = self.air_Vx_75[-1] -0.00004*700*self.air_Vx_75[-1]*self.dt
            air_tmp2_75 = self.air_Vy_75[-1] -self.g* self.dt-0.00004*700*self.air_Vy_75[-1]*self.dt
            air_tmp3_75 = self.air_x_75[-1] + self.air_Vx_75[-1]* self.dt
            air_tmp4_75 = self.air_y_75[-1] + self.air_Vy_75[-1]* self.dt
            self.air_Vx_75.append(air_tmp1_75)
            self.air_Vy_75.append(air_tmp2_75)
            self.air_x_75.append(air_tmp3_75)
            self.air_y_75.append(air_tmp4_75)
            
            
            if (air_tmp4_75<0):
                break
        air_x1_75 = self.air_x_75[-2]
        air_y1_75 = self.air_x_75[-2]
        air_x2_75 = self.air_y_75[-1]
        air_y2_75 = self.air_y_75[-1]    
        air_temp_75 = air_x1_75 - (air_y1_75) * ((air_x2_75 - air_x1_75)/(air_y2_75 - air_y1_75))
        self.air_x_75[-1] = air_temp_75
        self.air_y_75[-1] =          0
        
                    
    def show_results(self):
        plot1,=pl.plot(self.x_45, self.y_45,'r')
        plot2,=pl.plot(self.x_15, self.y_15,'g')
        plot3,=pl.plot(self.x_75, self.y_75,'b')
        plot4,=pl.plot(self.air_x_45, self.air_y_45,'lightblue')
        plot5,=pl.plot(self.air_x_15, self.air_y_15,'lightgreen')
        plot6,=pl.plot(self.air_x_75, self.air_y_75,'y')
        pl.title('cannon with air resistance')
        first_legend=pl.legend([plot1, plot2,plot3,plot4, plot5,plot6], ['45', '15','75','air45','air15','air75'], loc="best") 
        pl.show()
        
a = cannon()
a.calculate()
a.show_results()
```
#### 程序有点复杂，给修改造成很大阻碍，需要简化 
