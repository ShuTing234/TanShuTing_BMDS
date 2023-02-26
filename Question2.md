**2.1**  

Equation1: dES/ dt = k1*E*S – (k2+k3)ES  

Equation2: dP / dt = k3*ES

Equation3: dS / dt = k2ES - k1*E*S

Equation4: dE/ dt = (k2 + k3)ES - k1*E*S 

From Equation 1 & 4, dE/dt + dES/dt=0
Hence E(t)=E0- ES(t)  (Equation 5)
Substituting Equation 5 into equation 1 & 3:

Equation1=>  dES/ dt = k1*( E0- ES(t)  )*S – (k2+k3)ES  
	
	dES/ dt = k1*( E0- ES(t)  )*S – k2*ES- k3*ES
	
	dES/ dt = k1*( E0- ES(t)  )*S – k2*ES - dP/dt

Equation3 => dS / dt = k2ES - k1*( E0- ES(t)  )*S

Combining both, dES/dt= -dS/dt- dP/dt 

	dPdt= -dS/dt- dES/dt

According to Runge-kutta 4th order : yi+1= yi + 1/6(k1+2k2+2k3+2k4), where: 

k1 = hf(x0, y0)

k2 = hf[x0 + (½)h, y0 + (½)k1]

k3 = hf[x0 + (½)h, y0 + (½)k2]

k4 = hf(x0 + h, y0 + k3)


```
import numpy as np

E0=1
S0=10
ES0=0
P0=0
k1=100
k2=600
k3=150
time= np.arange(1,10,0.2)

dESdt = lambda k1,k2,k3,E0,ES,S: k1*( E0- ES)*S - (k2+k3)*ES  
dSdt= lambda k1,k2,E0,ES,S: k2*ES - k1*( E0- ES)*S
dEdt = lambda k1,k2,k3,ES,E,S: (k2 + k3)*ES - k1*E*S
dPdt = lambda k3,ES: k3*ES

data_mat= np.zeros((len(time),4))
data_mat[0]= [S0,E0,ES0, P0]

for t in range(len(time)):
    k1=h*f()
    k2 = hf[x0 + 0.5*h, y0 + 0.5*k1]
    k3 = hf[x0 + 0.5*h, y0 + 0.5k2]
    k4 = hf(x0 + h, y0 + k3)
    
    dES/ dt = k1*( E0- ES(t)  )*S – (k2+k3)ES  
    
    ESt= ES[t-1] + 1/6(k1+2k2+2k3+2k4)
  
