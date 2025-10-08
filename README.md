# 4-bit-Ripple-counter-using-Function-and-4-bit-Ripple-Adder-using-task

# Aim
To design and simulate a 4-bit-Ripple-counter-using-Function-and-4-bit-Ripple-Adder-using-task using Verilog HDL, and verify its functionality through a testbench in the Vivado 2023.1 environment. 

# Apparatus Required
Vivado 2023.1
# Procedure
1. Launch Vivado 2023.1
Open Vivado and create a new project.
2. Design the Verilog Code
Write the Verilog code for the seven-segment display, defining the logic that maps a 4-bit binary input to the corresponding segments (a to g) of the display.
3. Create the Testbench
Write a testbench to simulate the seven-segment display behavior. The testbench should apply various 4-bit input values and monitor the corresponding output.
4. Create the Verilog Files
Create both the design module and the testbench in the Vivado project.
5. Run Simulation
Run the behavioral simulation to verify the output. 
6. Observe the Waveforms
Analyze the output waveforms in the simulation window, and verify that the correct segments light up for each digit.
7. Save and Document Results
Capture screenshots of the waveform and save the simulation logs. These will be included in the lab report.

# Block Diagram

# 4-bit-Ripple-counter

<img width="850" height="254" alt="image" src="https://github.com/user-attachments/assets/2fd787a7-cd8b-454f-8d9b-58e43e0ee534" />


# 4-bit-Ripple-Adder

<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/cb43b11e-8e5e-4d3b-b9c1-537ca5d05ee8" />


# Verilog Code
# 4 bit Ripple Adder using Task

```
module rca (
    input [3:0] A, B,
    input Cin,
    output reg [3:0] Sum,
    output reg Cout
);
    reg c;
    integer i;

    task full_adder;
        input a, b, cin;
        output s, cout;
        begin
            s = a ^ b ^ cin;
            cout = (a & b) | (b & cin) | (a & cin);
        end
    endtask

    always @(*) begin
        c = Cin;
        for (i = 0; i < 4; i = i + 1) begin
            full_adder(A[i], B[i], c, Sum[i], c);
        end
        Cout = c;
    end
endmodule
```

# Test Bench

```
module rca_tb;
    reg [3:0] A, B;
    reg Cin;
    wire [3:0] Sum;
    wire Cout;

    rca uut (
        .A(A),
        .B(B),
        .Cin(Cin),
        .Sum(Sum),
        .Cout(Cout)
    );

    initial begin
        A = 4'b0000;
        B = 4'b0000;
        Cin = 0;
        #10 
        A = 4'b0011; 
        B = 4'b0101; 
        Cin = 0;
        #10 
        A = 4'b1111; 
        B = 4'b0001; 
        Cin = 1;
        #10 
        A = 4'b1010; 
        B = 4'b0101; 
        Cin = 0;
        #10 
        A = 4'b1111; 
        B = 4'b1111; 
        Cin = 0;
        #10 
        $finish;
    end
endmodule
```

# Output Waveform

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/34b5bb3c-a4c5-47ce-bbda-3d8636195703" />


# 4 bit Ripple counter using Function

```
module ripple_counter_func (
    input clk, rst,
    output reg [3:0] Q
);

    function [3:0] count;
        input [3:0] val;
        begin
            count = val + 1;
        end
    endfunction

    always @(posedge clk or posedge rst) begin
        if (rst)
            Q <= 4'b0000;
        else
            Q <= count(Q);
    end
endmodule
```

# Test Bench

```
module ripple_counter_func_tb;
    reg clk_t, rst_t;
    wire [3:0] Q_t;

    ripple_counter_func uut (
        .clk(clk_t),
        .rst(rst_t),
        .Q(Q_t)
    );

    initial clk_t = 0;
    always #5 clk_t = ~clk_t;

    initial begin
        rst_t = 1;
        #15 
        rst_t = 0;
        #100 
        $finish;
    end
endmodule
```

# Output Waveform 

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/497f2231-b9c6-4f37-95f0-e179167876ab" />


# Conclusion
In this experiment, a 4-bit-Ripple-counter-using-Function-and-4-bit-Ripple-Adder-using-task was successfully designed and simulated using Verilog HDL.
