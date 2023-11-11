![image](https://github.com/dishak14/pes_4bcounter/assets/92496153/dea69c11-1c9d-4aa3-bd56-b5df0530dc64)

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

## Floorplan

* In the openlane shell , execute the command ```run_floorplan```.

![floorplan](https://github.com/dishak14/pes_4bcounter/assets/92496153/7b913309-60c5-4b19-8495-bdb56cc3ed05)

* Checking in the ```OpenLane/designs/pes_counter3/runs/RUN_2023.11.03_03.59.42/results/floorplan``` directory if a .def file exists.

![floorplan2](https://github.com/dishak14/pes_4bcounter/assets/92496153/40cf8363-37b3-4b85-a5f0-61c68d56480d)

* As it exists, we will run the command ```magic -T /home/disha/Downloads/sky130A.tech lef read ../../tmp/merged.nom.lef def read pes_counter3.def &``` to view the layout on magic.
  
![floorplanlayout](https://github.com/dishak14/pes_4bcounter/assets/92496153/93372eb2-717c-4656-a771-a5df18a7a4e0)

  
![floorplanlayout1](https://github.com/dishak14/pes_4bcounter/assets/92496153/0b5ae9b2-be8f-45e1-ba40-c2ed430e484c)


![floorplanlayout2](https://github.com/dishak14/pes_4bcounter/assets/92496153/aa1cef82-7c3b-4128-b68f-9c993d311705)

## Placement

```run_placement```

![placement](https://github.com/dishak14/pes_4bcounter/assets/92496153/2510a7aa-170b-4f0c-90bf-0fade50f86f4)

![placement1](https://github.com/dishak14/pes_4bcounter/assets/92496153/25c5ae3d-e351-4875-a1fb-f892fc79060e)


![placement2](https://github.com/dishak14/pes_4bcounter/assets/92496153/6fef7acf-46e9-4437-ae2e-a5c4aa9d004e)

![floorplan3](https://github.com/dishak14/pes_4bcounter/assets/92496153/bbb69670-d7e7-49f1-a9a7-6c76b25023e9)



## Clock Tree Synthesis 

![run_ccts](https://github.com/dishak14/pes_4bcounter/assets/92496153/ce2ed980-aba5-4631-8dcb-b69333082fcd)

skew report


![cts1](https://github.com/dishak14/pes_4bcounter/assets/92496153/0ee6f8b6-02c6-431a-a81a-f3d0baeb7a75)

![cts2](https://github.com/dishak14/pes_4bcounter/assets/92496153/208292c5-5699-4be9-bcfb-5aa905a6d5b9)


![cts333](https://github.com/dishak14/pes_4bcounter/assets/92496153/06bd56e3-19ad-4018-9319-5c728499c76c)


## Routing

```run_routing```

![routing](https://github.com/dishak14/pes_4bcounter/assets/92496153/56d32fad-8518-4e16-bed2-ca0f9fa4d276)





![routing2](https://github.com/dishak14/pes_4bcounter/assets/92496153/024520e3-6b85-4cab-8554-c6fa9bd50c44)



![Screenshot from 2023-11-05 11-21-33](https://github.com/dishak14/pes_4bcounter/assets/92496153/ca144428-13a8-4637-a0d5-ba457b4f33ee)


![Screenshot from 2023-11-05 11-22-05](https://github.com/dishak14/pes_4bcounter/assets/92496153/a0c45bf2-1b3c-4bb8-bded-e23c3a2f586b)






![everything](https://github.com/dishak14/pes_4bcounter/assets/92496153/0d5999a4-320a-4eb3-ab8e-789c27b68fca)

![proper](https://github.com/dishak14/pes_4bcounter/assets/92496153/6dad56a3-e24b-41dc-85e1-bffabb3febf2)







</details>
