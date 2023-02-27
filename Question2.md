# Question 2.1

Equation1: $\frac{dES}{dt} = k_{1} \cdot S \cdot E   –  (k_{2}+k_{3})ES  $

Equation2: $\frac{dP}{dt} = k_{3} \cdot ES$

Equation3: $\frac{dS}{dt} = k_{2} \cdot ES - k_{1} \cdot E \cdot S$

Equation4: $\frac{dE}{dt} = (k_{2} + k_{3})ES - k_{1} \cdot E \cdot S $



# Question 2.2  

From above Equation 1 & 4, $\frac{dE}{dt} + \frac{dES}{dt} =0 $

Hence $E(t)=E_{0}- ES(t) $ 

Substituting into equation 1 & 3:

Equation1=> 

$\frac{dES}{dt} = k_{1}( E_{0} - ES(t)) S – ( k_{2}+k_{3} ) ES $  
	
$\frac{dES}{dt} = k_{1}( E_{0} - ES(t)) S – k_{2}ES+k_{3}ES $  
	
$\frac{dES}{dt} = k_{1} ( E_{0} - ES(t)  )  S – k_{2} ES - \frac{dP}{dt} $

Equation3 => 
$\frac{dS}{dt} = k_{2}ES - k_{1} ( E_{0}- ES(t)  )S $

Combining both, 
$\frac{dES}{dt} = -\frac{dS}{dt} - \frac{dP}{dt} $

$\frac{dP}{dt} = -\frac{dS}{dt}- \frac{dES}{dt} $

### According to Runge-kutta 4th order, 
$y_{i+1} = y_{i} + \frac{1}{6} (k_{1}+2k_{2}+2k_{3}+2k_{4}) $, where: 

- $k_{1} = hf(x0, y0)$

- $k_{2} = hf[x_{0} + (½)h, y_{0} + (½)k_{1}]$

- $k_{3} = hf[x_{0} + (½)h, y_{0} + (½)k_{2}]$

- $k_{4} = hf(x_{0} + h, y_{0} + k_{3})$


```
import numpy as np
import matplotlib as plt
E0=1
S0=10
ES0=0
P0=0
k1=100
k2=600
k3=150
time= np.arange(1,10,0.2)

dESdt = lambda k1,k2,k3,E,ES,S: k1*( E- ES)*S - (k2+k3)*ES  
dSdt= lambda k1,k2,E,ES,S: k2*ES - k1*( E- ES)*S
dEdt = lambda k1,k2,k3,ES,E,S: (k2 + k3)*ES - k1*E*S
dPdt = lambda k3,ES: k3*ES

data_mat= np.zeros((len(time),4)) # [S,E,ES,P] at each time, t
data_mat[0]= [S0,E0,ES0, P0]

for x in range(len(time)):
    t= time[x]
    h= time[x]- time[x-1]
    Si,Ei,ESi,Pi= data_mat[x-1,:]
    h= t-t0 
  
 '''   
    k1=  dESdt(k1,k2,k3,Ei,ESi,Si)    # couldn't solve the equation
    k2 = hf[time[x-1] + 0.5*h, ESi + 0.5*k1]
    k3 = hf[time[x-1] + 0.5*h, ESi + 0.5k2]
    k4 = hf(time[x-1] + h, ESi + k3)
 '''    
    ESt= ESi + 1/6(k1+2k2+2k3+2k4)
        
 '''   
    k1=  dSdt(k1,k2,Ei,ESi,Si)    # couldn't solve the equation
    k2 = hf[time[x-1] + 0.5*h, Si + 0.5*k1]
    k3 = hf[time[x-1] + 0.5*h, Si + 0.5k2]
    k4 = hf(time[x-1] + h, Si + k3)
 '''    
    St= Si + 1/6(k1+2k2+2k3+2k4)

 '''   
    k1=  dEdt(k1,k2,k3, ESi,Ei,Si)    # couldn't solve the equation
    k2 = hf[time[x-1] + 0.5*h, Ei + 0.5*k1]
    k3 = hf[time[x-1] + 0.5*h, Ei + 0.5k2]
    k4 = hf(time[x-1] + h, Ei + k3)
 '''    
    Et= Ei + 1/6(k1+2k2+2k3+2k4)

 '''   
    k1=  dPdt(k3, ESi)    # couldn't solve the equation
    k2 = hf[time[x-1] + 0.5*h, Pi + 0.5*k1]
    k3 = hf[time[x-1] + 0.5*h, Pi + 0.5k2]
    k4 = hf(time[x-1] + h, Pi + k3)
 '''    
    Pt= Pi + 1/6(k1+2k2+2k3+2k4)
    
    data_mat[x,:] = [St,Et,ESt,Pt]


plt.plot(time, data_mat[:,1], label = "S")
plt.plot(time, data_mat[:,2], label = "E")
plt.plot(time, data_mat[:,3], label = "ES")
plt.plot(time, data_mat[:,4], label = "P")
plt.xlabel('Time')
plt.ylabel('Concentration (uM)')
plt.legend()
plt.show()
```
