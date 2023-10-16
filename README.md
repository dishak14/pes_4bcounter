# pes_4bcounter

module tb_counter;

    // Inputs
    reg Clk;
    reg reset;
    reg UpOrDown;

    // Outputs
    wire [3:0] Count;

    // Instantiate the Unit Under Test (UUT)
    iiitb_4bbc uut (
        .Clk(Clk), 
        .reset(reset), 
        .UpOrDown(UpOrDown), 
        .Count(Count)
    );

    // Generate clock with 10 ns clk period.
    initial Clk = 0;
    always #5 Clk = ~Clk;

    initial begin
        // Add $dumpfile and $dumpvars
        $dumpfile("output.vcd"); // Specify the name of the VCD file
        $dumpvars(0); // Dump all signals

        // Apply Inputs
        reset = 0;
        UpOrDown = 0;
        #300;
        UpOrDown = 1;
        #300;
        reset = 1;
        UpOrDown = 0;
        #100;
        reset = 0;  
    end

endmodule
