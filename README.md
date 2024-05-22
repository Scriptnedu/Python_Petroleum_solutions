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
    
     

