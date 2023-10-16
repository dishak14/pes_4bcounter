# 4 BIT UP - DOWN COUNTER

## INTRODUCTION

In this repository we have followed the rtl to tapeout flow for a 4 bit up down counter. 

A 4-bit up-down counter is a digital electronic circuit capable of counting and displaying numerical values in a range of 0 to 15, using four binary bits. It is a fundamental component in digital electronics and microcontroller applications, often used for tasks such as controlling LED displays, address generation in memory devices, and as a key building block for more complex sequential logic systems.

This counter can operate in two modes: up-counting and down-counting. In the up-counting mode, it increments its value sequentially from 0 to 15, and in the down-counting mode, it decrements from 15 back to 0. The direction of counting is determined by a control input. The counter features a clock input, which controls the speed of counting and synchronization with other components in the system.

The code for 4 bit up down counter is written in the Hardware Discriptive Language (Verilog). The code has been provided in the files for this repository. We have written a testbench file in verilog to test the simulation results for our 4 bit up down counter.

## SIMULATION RESULTS 

In order to compile the verilog design file and the verilog test bench file we have used the command

```iverilog 4bcounter.v 4bcounter_tb.v```

 This creates a ./a.out file in our directory 

![image](https://github.com/dishak14/pes_4bcounter/assets/92496153/4d7382f9-3999-4c0c-b662-a407c05b95f0)

run ```./a.out``` on the terminal to get the output.vcd file.

Now we will run this output.vcd file on gtkwave using the command 

```gtkwave output.vcd```

Hence, we get the following simulation results

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








