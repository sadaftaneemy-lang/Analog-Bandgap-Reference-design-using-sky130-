This is my B.E Final year project
# Analog Bandgap Reference design using sky130

The 
## What is BGR ?
Bandgap  reference circuit is an analog Ip block . It provides constant reference voltage irrespective of temperature , supply voltage and process  variations. It is used in a number of analog and mixed circuit such as LDO , ADC, DAC.
A bandgap reference circuit utilizes a combination of transistors and resistors to create a voltage  that’s   independent of these factors as shown in figure below

<img width="394" height="222" alt="image" src="https://github.com/user-attachments/assets/1d6112c0-43d8-4220-981b-d801833466be" />

In a BGR (Bandgap Reference) circuit, CTAT (Complementary to Absolute Temperature) and PTAT (Proportional to Absolute Temperature) circuits are combined to create a temperature-stable reference voltage as shown in Fig

<img width="447" height="204" alt="image" src="https://github.com/user-attachments/assets/90781d59-a733-44fe-92f3-009c7c19ee08" />

The BGR leverages the opposite temperature characteristics of CTAT and PTAT to compensate for each other, resulting in a voltage that is relatively insensitive to temperature variations.  
CTAT part has negative temperature co-efficient that is decrease with increase temperature. Where as PTAT has positive temperature co-efficient that is increase with arising temperature.

## Complementary To Absolute Temperature (CTAT)

<img width="569" height="243" alt="image" src="https://github.com/user-attachments/assets/dd6bb40d-99af-48fa-9b09-c8601c8339a5" />

CTAT stands complementary to absolute temperature.It consists of current source connected to Vdd and diode connected to gnd  as shown in fig 
• VD = VT ln( I0/Is) .  
• Here VT stands for  Thermal Voltage 

As the temperature increases the value of CTAT decreases.As we can see in below fig.. It is a CTAT slope.

<img width="530" height="288" alt="image" src="https://github.com/user-attachments/assets/6b6fa842-0008-4ca8-8a9a-d817a9666b59" />

 ## Proportional To Absolute Temperature (PTAT) : 

<img width="582" height="228" alt="image" src="https://github.com/user-attachments/assets/d463ff22-2d3d-4081-87c1-feeed9d4f610" />

• PTAT -  stands proportional to absolute temperature.  
• It is  circuit current source connected to  Vdd  and  resistor and  number  of  Vdd  connected to gnd. 
The below figure is a plot of PTAT.

<img width="592" height="320" alt="image" src="https://github.com/user-attachments/assets/3737ffe3-2d28-43e2-a985-7fd88f563d3e" />

the graph shows the output vs temperature from –40°C to +140°C.
Output increases linearly with temperature.This is typical of a PTAT circuit or temperature-dependent 
device. 
• The straight red line indicates good linearity with temperature.

## Installation
For my project I have installed 3 opensource tools 
  1. NgSpice
  2. Magic Tool
  3. Sky130 PDK


## BANDGAP









