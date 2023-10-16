# 4 BIT UP - DOWN COUNTER

## INTRODUCTION

In this repository we have followed the rtl to tapeout flow for a 4 bit up down counter. The code for 4 bit up down counter is written in the Hardware Discriptive Langugae Verilog. The code has been provided in the files for this repository. We have written a testbench file in verilog to test the simulation results for our 4 bit up down counter.

# SIMULATION RESULTS 

In order to compile the verilog design file and the verilog test bench file we have used the command

```iverilog 4bcounter.v 4bcounter_tb.v```

 This creates a ./a.out file in our directory 

![image](https://github.com/dishak14/pes_4bcounter/assets/92496153/4d7382f9-3999-4c0c-b662-a407c05b95f0)

run ```./a.out``` on the terminal to get the output.vcd file.

Now we will run this output.vcd file on gtkwave using the command 

```gtkwave output.vcd```

Hence, we get the following simulation results



