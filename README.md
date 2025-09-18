# SIMULATION AND IMPLEMENTATION OF 4:1 MULTIPLEXER

## AIM
To design and simulate a 4:1 Multiplexer (MUX) using Verilog HDL in four different modeling styles—Gate-Level, Data Flow, Behavioral, and Structural—and to verify its functionality through a testbench using the Vivado 2023.1 simulation environment. The experiment aims to understand how different abstraction levels in Verilog can be used to describe the same digital logic circuit and analyze their performance.

## APPARATUS REQUIRED
- **Vivado 2023.1**

## Procedure

1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** and give a name (e.g., `Mux4_to_1`).  
3. Add/create your Verilog files and testbench.  
4. Select an FPGA part (e.g., `xc7a35ticsg324-1L`).  
5. Run **Synthesis** to check for errors.  
6. Run **Simulation** → **Run Behavioral Simulation**.  
7. Observe the waveforms of inputs and outputs.  
8. Adjust simulation time if needed (e.g., 1000ns).  
9. Save the project and take screenshots of results.  
10. Close simulation.  

---

## Logic Diagram
![image](https://github.com/user-attachments/assets/d4ab4bc3-12b0-44dc-8edb-9d586d8ba856)

---

## Truth Table
![image](https://github.com/user-attachments/assets/c850506c-3f6e-4d6b-8574-939a914b2a5f)

---

## Verilog Code

### 4:1 MUX Gate-Level Implementation
```verilog
/module MUX4_1_GATE (
    input wire A,
    input wire B,
    input wire C,
    input wire D,
    input wire S0,
    input wire S1,
    output wire Y
 );
    wire not_S0, not_S1;
    wire A_and, B_and, C_and, D_and;
    not (not_S0, S0);
    not (not_S1, S1);
    and (A_and, A, not_S1, not_S0);
    and (B_and, B, not_S1, S0);
    and (C_and, C, S1, not_S0);
    and (D_and, D, S1, S0);
    or (Y, A_and, B_and, C_and, D_and);
 endmodule
```
### 4:1 MUX Gate-Level Implementation- Testbench
```verilog
`timescale 1ns / 1ps
module mux4_to_1_tb;

    reg A, B, C, D;
    reg S0, S1;
    wire Y;

    mux4_to_1_gate uut (
        .A(A), .B(B), .C(C), .D(D),
        .S0(S0), .S1(S1),
        .Y(Y)
    );

    initial begin
        A = 0; B = 0; C = 0; D = 0; S0 = 0; S1 = 0;
        #10 A=1; S1=0; S0=0;
        #10 B=1; A=0; S1=0; S0=1;
        #10 C=1; B=0; S1=1; S0=0;
        #10 D=1; C=0; S1=1; S0=1;
        #10 $stop;
    end

    initial begin
        $monitor("Time=%0t | S1=%b S0=%b | A=%b B=%b C=%b D=%b | Y=%b",
                  $time, S1, S0, A, B, C, D, Y);
    end

endmodule
```
## Simulated Output Gate Level Modelling

<img width="1195" height="673" alt="Gate" src="https://github.com/user-attachments/assets/4b79f59b-1c65-42d3-9630-ea0e2783b83e" />

---
### 4:1 MUX Data flow Modelling
```verilog
module MUL4_1_DATA (
    input wire A,
    input wire B,
    input wire C,
    input wire D,
    input wire S0,
    input wire S1,
    output wire Y
 );
    assign Y = (~S1 & ~S0 & A) |
               (~S1 & S0 & B) |
               (S1 & ~S0 & C) |
               (S1 & S0 & D);
 endmodule
 

```
### 4:1 MUX Data flow Modelling- Testbench
```verilog
`timescale 1ns / 1ps
module mux4_to_1_tb;

    reg A, B, C, D;
    reg S0, S1;
    wire Y;

    mux4_to_1_gate uut (
        .A(A), .B(B), .C(C), .D(D),
        .S0(S0), .S1(S1),
        .Y(Y)
    );

    initial begin
        A = 0; B = 0; C = 0; D = 0; S0 = 0; S1 = 0;
        #10 A=1; S1=0; S0=0;
        #10 B=1; A=0; S1=0; S0=1;
        #10 C=1; B=0; S1=1; S0=0;
        #10 D=1; C=0; S1=1; S0=1;
        #10 $stop;
    end

    initial begin
        $monitor("Time=%0t | S1=%b S0=%b | A=%b B=%b C=%b D=%b | Y=%b",
                  $time, S1, S0, A, B, C, D, Y);
    end

endmodule

```
## Simulated Output Dataflow Modelling

<img width="1349" height="757" alt="Data" src="https://github.com/user-attachments/assets/9291c320-9497-40b1-b910-12bb4cf185ff" />

---
### 4:1 MUX Behavioral Implementation
```verilog
 module MUX4_1_BEHAVIORAL(
    input wire A,
    input wire B,
    input wire C,
    input wire D,
    input wire S0,
    input wire S1,
    output reg Y
    );
    always @(*) begin
        case ({S1, S0})
            2'b00: Y = A;
            2'b01: Y = B;
            2'b10: Y = C;
            2'b11: Y = D;
            default: Y = 1'bx;
        endcase
    end
 endmodule
```
### 4:1 MUX Behavioral Modelling- Testbench
```verilog
/`timescale 1ns / 1ps
module mux4_to_1_tb;

    reg A, B, C, D;
    reg S0, S1;
    wire Y;

    mux4_to_1_gate uut (
        .A(A), .B(B), .C(C), .D(D),
        .S0(S0), .S1(S1),
        .Y(Y)
    );

    initial begin
        A = 0; B = 0; C = 0; D = 0; S0 = 0; S1 = 0;
        #10 A=1; S1=0; S0=0;
        #10 B=1; A=0; S1=0; S0=1;
        #10 C=1; B=0; S1=1; S0=0;
        #10 D=1; C=0; S1=1; S0=1;
        #10 $stop;
    end

    initial begin
        $monitor("Time=%0t | S1=%b S0=%b | A=%b B=%b C=%b D=%b | Y=%b",
                  $time, S1, S0, A, B, C, D, Y);
    end

endmodule

```
## Simulated Output Behavioral Modelling
<img width="1348" height="757" alt="Behavioral" src="https://github.com/user-attachments/assets/12be12fd-670b-4c4a-8fd3-5715cfa6fe00" />



### 4:1 MUX Structural Implementation

![image](https://github.com/user-attachments/assets/eea81c2c-7dfa-43aa-9cea-1ab4ed54db6c)


```verilog
module mux2_to_1 (
    input wire A,
    input wire B,
    input wire S,
    output wire Y
);
    assign Y = S ? B : A;
endmodule

module mux4_to_1_structural (
    input wire A,
    input wire B,
    input wire C,
    input wire D,
    input wire S0,
    input wire S1,
    output wire Y
);
  wire mux_low, mux_high;
    mux2_to_1 mux0 (.A(A), .B(B), .S(S0), .Y(mux_low));
    mux2_to_1 mux1 (.A(C), .B(D), .S(S0), .Y(mux_high));
    mux2_to_1 mux_final (.A(mux_low), .B(mux_high), .S(S1), .Y(Y));
 endmodule

```
### Testbench Implementation
```verilog
 `timescale 1ns / 1ps
module mux4_to_1_tb;

    reg A, B, C, D;
    reg S0, S1;
    wire Y;

    mux4_to_1_gate uut (
        .A(A), .B(B), .C(C), .D(D),
        .S0(S0), .S1(S1),
        .Y(Y)
    );

    initial begin
        A = 0; B = 0; C = 0; D = 0; S0 = 0; S1 = 0;
        #10 A=1; S1=0; S0=0;
        #10 B=1; A=0; S1=0; S0=1;
        #10 C=1; B=0; S1=1; S0=0;
        #10 D=1; C=0; S1=1; S0=1;
        #10 $stop;
    end

    initial begin
        $monitor("Time=%0t | S1=%b S0=%b | A=%b B=%b C=%b D=%b | Y=%b",
                  $time, S1, S0, A, B, C, D, Y);
    end

endmodule
```
## Simulated Output Structural Modelling

<img width="1351" height="758" alt="Structural" src="https://github.com/user-attachments/assets/13c8d4c5-79f0-46e0-928f-adf00fb565b3" />

---
### CONCLUSION

In this experiment, a 4:1 Multiplexer was successfully designed and simulated using Verilog HDL across four different modeling styles: Gate-Level, Data Flow, Behavioral, and Structural.The simulation results verified the correct functionality of the MUX, with all implementations producing identical outputs for the given input conditions.

