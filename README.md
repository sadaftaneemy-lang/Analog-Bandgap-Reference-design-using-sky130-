*This is my B.E Final year project (2025-2026)* 
# Analog Bandgap Reference design using sky130

🎯 The objective of this project is to design and analyze a Bandgap Reference (BGR) circuit capable of generating a stable reference voltage that remains nearly constant despite variations in temperature, supply voltage, and process parameters.

## 🧠 What is BGR ?
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

## 🔧 Installation

For my project I have installed 3 opensource tools 
  1. NgSpice
  2. Magic Tool
  3. Sky130 PDK

**Ngspice installation** :     

```bash id="v9vqu3"
sudo apt-get install-y ngspice

```
**Magic Tool** :

```bash id="v9vqu3"
sudo wget "http://opencircuitdesign.com/magic/archive/magic-8.3.122.tgz"

tar-xvzf magic-8.3.122.tgz

cd magic-8.3.122

sudo ./configure

sudo make

sudo make install

```


**Sky130 PDK** :

```bash id="v9vqu3"
git clone git://opencircuitdesign.com/open_pdks

cd open_pdks

sudo ./configure--enable-sky130-pdk=/home/sadaf/Desktop/webinar/pdks/skywaterpdk/libraries--with-sky130-local-path=/home/sadaf/Desktop/webinar/pdks

sudo make

sudo make install

```
## BANDGAP REFERENCE CIRCUIT

**Below is the design of the BGR circuit**

<img width="681" height="494" alt="image" src="https://github.com/user-attachments/assets/a1fc4b56-2ef7-4144-b035-b9bb8c7f4a99" />

## This is the SPICE Netlist
<img width="996" height="443" alt="image" src="https://github.com/user-attachments/assets/eabc1f62-500d-403b-a569-24b6b0fe41c4" />

<img width="989" height="533" alt="image" src="https://github.com/user-attachments/assets/957c8bcf-14d2-4fc8-be78-6987bc4f7b65" />

First line is a comment line 

Third line Saves the branch current 

4th & 5th line gives the address of libraries which will be used for simulation.

Now looking for circuit elements

**For MOSFETS** 

• First we will write name of transistor. 

• then the terminal. 

Ex: XM1  A C C VDD VDD 

Here XM1  is the name of Transistor 

A is Drain 

C is Gate 

VDD  is  source

VDD is substrate.

For XM1 the drain terminal is connected to A node, the gate terminal is connected to C node the source and Substrate are connected to VDD.

Next we write the model name of the transistor which we have used,and in the last of line we write length and width.

**For  BJT**  
Ex: X6 GND GND  I  GND 

First GND is Collector.

Second GND is Base.

I is Emitter

Third GND is substrate

In X6 as we can see only the emitter is Connected to the node and all other In X6 as we can see only the emitter is Connected to the node and all other terminals are connected to ground, so we have written GND GND  I and Ground.Next we have written the model name for the BJT. 

And lastly M=1 represents the Number of BJT connected to this node.

If a number of BJTS are connected to the Same terminals then we can write the number of BJTS connected to similar terminals,for the above sentence ex is X7 here we have 8 BJTS Connected to similar terminal have directly written M=8 in our code. 

**For Resistors** 
First we  write Resistor  name.

Then both  the terminals to which it is Connected 

Then it's value 

Ex: RL  GND  Vref  100MEG 

RL is the Resistor Name 

ND and Vref are both the terminal  to which it is connected. 
100 MEG  is value. 

In our code we have not given the value for R1, R2, R3 because further we will give the values and take out graphs.Voltage Sources V1, V2, V3 & V4 are given so that We can measure the current flowing through the branch.

I have connected VDDA to VDD and GND and it is DC voltage of 3.3V 

→VDDA  VDD  GND  DC  3.3V 

I  have also connected a DC voltage of 3.3v Source to enable to make it on 

→VD  En  GND  DC 3.3V 
 
.dc  temp -40  140  0.1 

↳ This line is used for DC analysis, it gives the temperature Switch from  -40 to 140 °C With step size of 0.1  


From line 45 to 53 are used for running the DC analysis.

All the plot are used and to plot the voltages which we want 
After running the netlist we  get plots of Vref, CTAT and PTAT.

