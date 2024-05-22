# Python_Petroleum_solutions
This repository is about solving unsteady-state flow problem using python programming language.


#### Problem Description

The objective is to use python programming language to carry out a basic transient (unsteady state) analysis. Under the steady-state flowing condition, the same quantity of fluid enters the flow system as leaves it. In unsteady-state flow condition, the flow rate into an element of volume of a porous media may not be the same as the flow rate out of that element. In this work, radial flow of slightly compressible fluid is considered narrowing it down to constant terminal rate solution.
The constant-terminal-rate solution is an integral part of most transient test analysis techniques, such as with drawdown and pressure buildup analyses. Most of these tests involve producing the well at a constant flow rate and recording the flowing pressure as a function of time, i.e., p(rw,t). There are two commonly used forms of the constant-terminal-rate solution:  
     (1) The Ei-function solution 
     (2) The dimensionless pressure pD solution.
Note: this work utilizes the Ei-function solution.


#### Sample Problem

An oil well is producing at a constant flow rate of 300 STB/day under unsteady-state flow conditions. The reservoir has the following rock and fluid properties: 
Bo = 1.25 bbl/STB
Ko = 60 md
Porosity = 15%
Viscosity = 1.5 cp
h = 15ft
rw =0.25 ft
ct = 12 * 10-6 psi-1
pi = 4000psi

1)calculate pressure at radii of 0.25, 5, 10, 50, 100, 500, 1000, 1500, 2000, and 2500 feet, for 1 hour

2)Repeat part 1 for t = 12 hours and 24 hours.


## Formulars used for the program

x = -(948*Φ*μ*ct*(r**2))/(k*t)
E = np.log(1.781*x)
p = 4000 + 44.125 * E

where:
    pi = 4000psi
    x = argument
    E = exponential integral
when: 
    x < 0.1, E = np.log(1.781*x)
    0.1<= x <= 10, E is obtained from the table
    x > 10 , E == 0
    
        
    


### importing important python libraies

#import requests
import numpy as np
import pandas as pd
import csv
import math as m

### defining variables and parameters

Φ = 0.15
μ = 1.5
ct = 12*10**(-6)
k = 60


table = {"x" :[0.1,0.2,0.3,0.4,0.5,0.6,0.7,0.8,0.9,1.0,1.1,1.2,1.3,1.4,1.5,1.6,1.7,1.8,1.9,2.0,2.1,2.2,2.3,2.4,2.5,2.6,2.7,2.8,2.9,
               3.0,3.1,3.2,3.3,3.4,3.5,3.6,3.7,3.8,3.9,4.0,4.1,4.2,4.3,4.4,4.5,4.6,4.7,4.8,4.9,5.0,5.1,5.2,5.3,5.4,5.5,5.6,5.7,5.8,
               5.9,6.0,6.1,6.2,6.3,6.4,6.5,6.6,6.7,6.8,6.9,7.0,7.1,7.2,7.3,7.4,7.5,7.6,7.7,7.8,7.9,8.0,8.1,8.2,8.3,8.4,8.5,8.6,
               8.7,8.8,8.9,9.0,9.1,9.2,9.3,9.4,9.5,9.6,9.7,9.8,9.9,10.0],
         "E(x)":  [-1.82292,-1.22265,-0.90568,-0.70238,-0.55977,-0.45438,-0.37377,-0.31060,-0.26018,-0.21938,-0.18599,-0.15841,-0.13545,
                -0.11622,-0.10002,-0.08631,-0.07465,-0.06471,-0.05620,-0.04890,-0.04261,-0.03719,-0.03250,-0.02844,-0.02491,-0.02185,-0.01918,-0.01686,-0.01482,-0.01305,-0.01149,
                 -0.01013,-0.00894,-0.00789,-0.00697,-0.00616,-0.00545,-0.00482,-0.00427,-0.00378,-0.00335,-0.00297,-0.00263,-0.00234,-0.00207,-0.00184,-0.00164,-0.00145,
                 -0.00129,-0.00115,-0.00102,-0.00091,-0.00081,-0.00072,-0.00064,-0.00057,-0.00051,-0.00045,-0.00040,-0.00036,-0.00032,-0.00029,
             -0.00026,-0.00023,-0.00020,-0.00018,-0.00016,-0.00014,-0.00013,-0.00012,-0.00010,-0.00009,-0.00008,-0.00007,-0.00007,-0.00006,-0.00005,
                -0.00005,-0.00004,-0.00004,-0.00003,-0.00003,-0.00003,-0.00002,-0.00002,-0.00002,-0.00002,-0.00002,-0.00001,-0.00001,-0.00001,-0.00001,-0.00001,
                -0.00001,-0.00001,-0.00001,-0.00001,-0.00001,-0.00000,-0.00000]}



### creating functions to perform calculation to obtain x

def calculate_x(r, t, Φ, μ, ct, k):
    return (948 * Φ * μ * ct * (r ** 2)) / (k * t)




### creating functions to perform calculation to obtain E 

def calculate_E(x, table):
    if x < 0.1:
        E = np.log(1.781 * x)
    elif 0.1 <= x <= 10:
        x = round(x,1)
        if x in table['x']:
            index = table['x'].index(x)
            E = table['E(x)'][index]
        else:
            print(f"Warning: x value {x} not in table")
            E = None 
    else:
        E = 0
    return E





### creating functions to perform calculation to obtain p and and getting result

def calculate_p(E):
    return 4000 + 44.125 * E



while True:
    try:
        r = float(input("Enter the radius of the well: "))
        t = int(input("Enter time in hours: "))
        break
    except ValueError:
        print("Error: Please enter valid numeric values.")

        
x = calculate_x(r, t, Φ, μ, ct, k)
print("x:", x)
E = round(calculate_E(x, table),2)
print("E:", E)


if E is not None:
    p = round(calculate_p(E),0)
    print(f"p: {p} psia")
else:
    print("Error: Could not calculate p due to missing E value.")

