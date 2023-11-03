# 4 BIT UP - DOWN COUNTER

## INTRODUCTION

In this repository we have followed the rtl to tapeout flow for a 4 bit up down counter. 

A 4-bit up-down counter is a digital electronic circuit capable of counting and displaying numerical values in a range of 0 to 15, using four binary bits. It is a fundamental component in digital electronics and microcontroller applications, often used for tasks such as controlling LED displays, address generation in memory devices, and as a key building block for more complex sequential logic systems.

This counter can operate in two modes: up-counting and down-counting. In the up-counting mode, it increments its value sequentially from 0 to 15, and in the down-counting mode, it decrements from 15 back to 0. The direction of counting is determined by a control input. The counter features a clock input, which controls the speed of counting and synchronization with other components in the system.

The code for 4 bit up down counter is written in the Hardware Discriptive Language (Verilog). The code has been provided in the files for this repository. We have written a testbench file in verilog to test the simulation results for our 4 bit up down counter.

<details><summary>RTL TO GDS </summary>
 
## SIMULATION RESULTS 

In order to compile the verilog design file and the verilog test bench file we have used the command

```iverilog 4bcounter.v 4bcounter_tb.v```

 This creates a ./a.out file in our directory 

![image](https://github.com/dishak14/pes_4bcounter/assets/92496153/4d7382f9-3999-4c0c-b662-a407c05b95f0)

run ```./a.out``` on the terminal to get the output.vcd file.

Now we will run this output.vcd file on gtkwave using the command 

```gtkwave output.vcd```

Hence, we get the following simulation results (Pre Synthesis simulation result )

![image](https://github.com/dishak14/pes_4bcounter/assets/92496153/cd254ea4-97ca-4100-8775-79689bd3ecd0)


## Synthesis result 

```yosys```

For reading the library : ```read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib```

For reading the design: ```read_verilog 4bcounter.v```

```synth -top iiit_4bbc.v```


![image](https://github.com/dishak14/pes_4bcounter/assets/92496153/35f560ac-6221-48dc-a705-210f8cff3d68)

For generating netlist : ```abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib```

![image](https://github.com/dishak14/pes_4bcounter/assets/92496153/e873d82d-66c2-4788-a744-b96808432f9a)

```show```

![image](https://github.com/dishak14/pes_4bcounter/assets/92496153/7d6a54ff-11af-4a79-84aa-a7d5376666b7)

## GLS Simulation

We run the .net file created after yosys synthesis and the testbench file using the iverilog command to generate a waveform and compare it with the waveform generated in the beginning.

we use the command : ``` iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v 4bcounter_net.v 4bcounter_tb.v ls ```

we again get the a.out file and we can run it on gtkwave as done previously to get the following results 

![image](https://github.com/dishak14/pes_4bcounter/assets/92496153/cd254ea4-97ca-4100-8775-79689bd3ecd0)



</details>

<details><summary> PHYSICAL DESIGN </summary>

# Physical Design using OpenLane
 
OpenLane is an open-source digital ASIC (Application-Specific Integrated Circuit) design flow framework used to automate the process of designing and fabricating digital integrated circuits. OpenLane aims to make custom ASIC design more accessible to a broader range of engineers and researchers.The goal of OpenLANE is to make the ASIC design flow more accessible to a broader community. By providing an open-source framework, it allows for collaboration, innovation, and knowledge sharing in the field of chip design. Additionally, it leverages the SkyWater 130nm process as a reference PDK, enabling users to create designs using this technology.
OpenLANE's automation helps reduce the barriers to ASIC design by providing a framework that streamlines the process.

For the physical design of the 4 bit counter, we will be working on a pdk variant called sky130_fd_sc_hd
* sky130 : is the process name
* fd : skywater foundary
* sc : standard cell
* hd(high density) : variant of pdk

## Preparing design directory for execution

* navigate to Openlane's design folder using ```cd Openlane/designs```.
* In this directory, make another directory which will be your design directory. In our case we have used ```mkdir pes_counter3```.
* In pes_counter3, write a config.json file.
  ![config](https://github.com/dishak14/pes_4bcounter/assets/92496153/fdb90120-0956-4a6a-889e-13090c2650da)
* Make another directory called src using ```mkdir src```. In this directory add your verilog design and give the same name as that of your directory (pes_counter3.v).
  By the end, your design ddirectory is supposed to look like this

![directory](https://github.com/dishak14/pes_4bcounter/assets/92496153/60df62c7-8fa7-4203-8b04-346e162e8a11)

## Opening Openlane terminal

* In the Openlane directory type, ```make mount```.
* Openlane contianer appears, type ```./flow.tcl -interactive```.
* Open openlane package using ```package require openlane 0.9```.

![openlane](https://github.com/dishak14/pes_4bcounter/assets/92496153/9447d164-8eec-44a5-9505-adb5d9cddad4)


## Synthesis 


* Use ```prep -design <design_directory>``` to prepare your design for running synthesis.
 

![prep_design](https://github.com/dishak14/pes_4bcounter/assets/92496153/47c3aca5-3df8-403f-8e03-b49bca9e6034)

* ```run_synthesis```
  
 ![synthesis](https://github.com/dishak14/pes_4bcounter/assets/92496153/b25ec04d-15c9-4594-b608-d980d5cf123f)

 Synthesis-log :

![synthesis1](https://github.com/dishak14/pes_4bcounter/assets/92496153/856e8eff-300d-426c-b303-008505351e5b)



![syyynthesis2](https://github.com/dishak14/pes_4bcounter/assets/92496153/0bec9d9b-87fa-4d3e-8e8d-60f18e295d1c)


![synthesis3](https://github.com/dishak14/pes_4bcounter/assets/92496153/c371cbe8-c46e-4427-9f96-8cb288cc1217)


![synthesis4](https://github.com/dishak14/pes_4bcounter/assets/92496153/f41837c8-ec94-4c71-a063-bc475d9f2591)

Sta-log

![stalog](https://github.com/dishak14/pes_4bcounter/assets/92496153/db8d9460-96e1-4af9-9e08-1f60329c9a6b)

![stalog2](https://github.com/dishak14/pes_4bcounter/assets/92496153/096c13ac-edb1-41bd-8f06-c92f1733f458)











</details>
