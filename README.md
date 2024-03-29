
<!--
  /*
   * webpage url
   *  https://mechaengbryan.github.io/
   */
-->

## California State University, Chico
## Mecahanical and Mechatronic Engineering
## MECA 482 Controls - Temperature Control System - Group Project Website
## MECA 440 Engineerinig Capstone - SLAC Reservoir Cooling System Modeling

<br/>
<br/>

### Project Description
<br/>
Leveraging our Senior Capstone Project’s problem, we are creating a mathematical model that will programmatically capture the temperature control system. Our project is being tasked with controlling the temperature of a 4” in length x 0.5” in diameter 316 Stainless Steel cylinder – this cylinder is used as a holding reservoir for samples used during experimentation. Initial conditions for the cylinder are standard laboratory conditions e.g. 24°C and 50% RH. The final condition for the cylinder is 4 +/- 0.25°C after 5 minutes i.e. must achieve an average -5°C/minute ramp rate


<br/>
<br/>
<br/>
<p align="center">
Testing setup
<br/>
The power supplies were used to power the Peltiers(x3) and the 80mm x 80mm Fans (x2)
<br/>
MATLAB and an Arduino were used to supply PWM signal to Fans for Fan Speed
<img src="Full_Setup.jpg" width="800" />

<br/>
<br/>
<p align="center">
Device Under Test (DUT)
</p>
<p align="center">
<img src="ClamShell.jpg" width="35%" />

<br/>
<br/>
<p align="center">
Parts list (not capturing clam shell)
</p>
<p align="center">
<img src="Parts.png" width="50%" />

<br/>
<br/>
<p align="center">
Performing Test
</p>
<p align="center">
<img src="Testing.jpg" width="50%" />

<br/>
<br/>
<p align="center">
DMM with K-Type Thermocouple Displaying Temperature
</p>
<p align="center">
<img src="Temperature.jpg" width="50%" />

<br/>
<br/>
<p align="center">
<br/>
The input step command can be ignored on this plot, because this was not a closed loop test
<br/>
Test initial Temperature was 24 degrees Centigrade - it took ~2 minutes to achieve 4 degrees Centigrade
<br/>
Sampling was performed using a stopwatch at 10 second intervals
</p>
<p align="center">
<img src="TEC_Testing.png" width="800" />
<p align="center">
Results Plotted with exponential curve fit
<p align="center">

<br/>
<br/>
<br/>
<br/>
<br/>

<p align="center">
The trend line equation was then taken from above collected data and converted to s domain
</p>
<p align="center">
<img src="Equations.png" width="50%" />
<p align="center">

<br/>
<br/>


### MATLAB Script used to analyze Transfer Function Response

<pre>

%MECA 482 - Thermal Response
%12/4/2019

clc; close all; clear all;

%% raw data from testing, sampled at .1Hz
temp = [22.2 21.7 20.2 17.9 15.4 13.2 11.1 8.9 7.2 6 4.5 3.2 2.7];

time = [10 20 30 40 50 60 70 80 90 100 110 120 130];

%% Transfer Function and step response
s = tf('s');
%init temperature from exp trend line at t = 0
t = 0;
To = 34.701*exp(-.018*t);
K = -34.701;            % DC gain
tau = .018^-1;
TF = K/(tau*s+1);        % model transfer function
[y,t] = step(TF,130);    % model step response

%% plot generation
plot(time,temp,'rx',t,y+To,'b')
xlabel('Time [sec]')
ylabel('Temperature [C]')
title('SLAC Reservoir Clamshell Temperature Step Response')
legend('Raw data','Model','Location','NorthEast')

</pre>

<br/>
<br/>
<br/>

<p align="center">
The results from the above MATLAB script plotted
</p>
<p align="center">
<img src="MATLAB_Script_Results.jpg" width="75%" />
<p align="center">

<br/>
<br/>
<br/>
<p align="center">
The below captures the implemented Closed Loop Temperature Contoller using Simulink
<br/>
<img src="Simulink.jpg" width="800" />




<br/>
<br/>
<br/>
<p align="center">
Data collected during testing of the system
<br/>
<img src="Testing_Collected_Temp_Data5.jpg" width="800" />


<br/>
<br/>
<br/>
<p align="center">
Unfortunately because of hardware limitations within the Arduino Uno we were using (32kb Flash memory) we were not able to compile and execute the simulink model on the microcontroller in a standalone configuration. Alternative microcontrollers have since been identified.

<br/>
<br/>
<br/>
<p align="center">
Link to prototype testing below
<br/>
<p align="center">
<a href="https://youtu.be/kgfhSX25HTA"
target="_blank"><img src="2019-12-09 22.28.17.jpg" 
alt="Prototype Testing" width="240" height="180" border="10" /></a>

