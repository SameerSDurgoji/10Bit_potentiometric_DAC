# 10Bit_potentiometric_DAC

# Introduction

Most of the signals around us, in the world we live in are not digital in nature, rather they are analog. The digital systems can understand only digital signals, not analog. Hence, it becomes important to interface the digital systems we the external analog world. The analog input signals are to be converted to digital signals using Analog to Digital Converters at the input end of the digital system. After the processing by the system, the digital signals are to be converted back into analog signals using Digital to Analog Converters. 

A n-bit Digital to Analog Converter (DAC) takes a n-bit digital word and converts it into a proportional analog voltage with respect to the reference voltage. The potentiometric DAC uses the concept of Voltage Divider. In an N-bit DAC, the analog voltage range, i.e. the Vref (here 3.3 V) is equally divided into 2^N voltage values. This is achieved by a series on 2^N equal resistors and taps are provided across each R. The combination of switches to tap the values is designed using the N-bit digital word as input. An example of N-bit potentiometric DAC is shown in the figure 1.

![generalDAC](https://github.com/SameerSDurgoji/10Bit_potentiometric_DAC/blob/main/Screenshots/circuit%20(1).png)

The switches are designed as shown in the figure 2. The digital voltage of 1.8V or 0V is given at the digital input port for logic 1 and 0 respectively. If the digital input is logic 1, then Vin1 appears at the output port, else Vin2 appears at the output. Hence this switch circuit replaces two switches in same level as it takes into account both the swiches of complemented and uncomplemented bit.

![switch circuit](https://github.com/SameerSDurgoji/10Bit_potentiometric_DAC/blob/main/Screenshots/switch%20circuit.png)

These designs are used for pre layout simulations.

# Pre Layout Simulations

The tools used for these simulations are:
* eSim
* ngspice

The schematics for a switch circuit and a 2 bit DAC were designed in eSim. As the analog input voltage was 3.3V, the vdd and vref was set to 3.3V. For the voltage divider circuit, a series of 4 resistors of 250ohm each were used. The model name of the PMOSFET used was sky130_fd_pr__pfet_g5v0d10v5. The model name of the NMOSFET used was sky130_fd_pr__nfet_03v3_nvt. To include the model files of these mosfets, a new spice file was created where the sky130_fd_pr__nfet_03v3_nvt__mismatch.corner.spice, sky130_fd_pr__nfet_03v3_nvt__tt.corner.spice, sky130_fd_pr__pfet_g5v0d10v5__mismatch.corner.spice, sky130_fd_pr__pfet_g5v0d10v5__tt.corner.spice, all.spice files were included.
This custom1.spice file should be placed in models folder in sky130_fd_pr.

For the 2 bit DAC, switch circuit was included as a subcircuit. After creating the schematics, the spice netlist was extracted. The necessary model files of sky130 tt transistors were included in the netlist and transient analysis was performed. The screenshots of the schematic are as shown below:

![switch](https://github.com/SameerSDurgoji/10Bit_potentiometric_DAC/blob/main/Screenshots/switch_eSim.png)


![2bitDAC](https://github.com/SameerSDurgoji/10Bit_potentiometric_DAC/blob/main/Screenshots/2bitDAC.png)

The subcircuit of the switch could not be properly included in the 2 bit DAC circuit. So, a spice netlist was newly created for the 2bit DAC and the transient analysis was performed. The result of transient analysis of the switch is shown below:

![switch op](https://github.com/SameerSDurgoji/10Bit_potentiometric_DAC/blob/main/Screenshots/switch_output.png)

The file switchfinal.spice was used.
Here, in the spice file, the higher reference voltage was set to 2.5V and the lower reference voltage was set to 2.2V just for the purpose of verifying the circuit. Here it can be observed that when the digital input for the switch is high (1.8V), the higher reference voltage appears at the output; when the digital input for the switch is low(0V), the lower reference voltage appears at the output. So, it was concluded that the switch circuit is working properly.

The result of the transient analysis of the 2bit DAC is shown below:

![2bit dac op](https://github.com/SameerSDurgoji/10Bit_potentiometric_DAC/blob/main/Screenshots/Screenshot_1.png)

The spice file 2bitDAC.spice was used.
The two bit digital inputs were given as 11, 10, 01 and 00. It can be observed that when the inputs are 1 1, 2.47V appears at the output. When the inputs are 1 0, 1.57 V appears at the output. Similarly, for the inputs 0 1 and 0 0, 0.76V and 0 V appear at output respectively. Thus, the 2 bit digital input is converted to corresponding analog values with reference voltage of 3.3 V.

# Further Work:

Further work would be to include the subcircuits of switch and the 2bit DAC to design DACs of higher resolution. 
