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
// Gate Level Modelling - Skeleton
module mux4_gate (
    input  wire I0, I1, I2, I3,
    input  wire S0, S1,
    output wire Y
);
    // Declare internal wires

    // Write NOT gates

    // Write AND gates

    // Write OR gate

endmodule

```
### 4:1 MUX Gate-Level Implementation- Testbench
```verilog
// Testbench Skeleton
`timescale 1ns/1ps
module tb_mux4_gate;

    // Declare testbench signals
    reg I0, I1, I2, I3;
    reg S0, S1;
    wire Y;

    // Instantiate DUT
    mux4_gate uut (
        .I0(I0), .I1(I1), .I2(I2), .I3(I3),
        .S0(S0), .S1(S1),
        .Y(Y)
    );

    initial begin
        // Initialize inputs

        // Apply test cases

        // Stop simulation
        #10 $stop;
    end

endmodule
```
## Simulated Output Gate Level Modelling

<img width="1195" height="673" alt="Gate" src="https://github.com/user-attachments/assets/cd9317c7-91b4-4828-96b5-73d5a3a7ec6f" />

---
### 4:1 MUX Data flow Modelling
```verilog
// Dataflow Modelling - Skeleton
module mux4_dataflow (
    input  wire I0, I1, I2, I3,
    input  wire S0, S1,
    output wire Y
);
    // Write assign statement using operators

endmodule

```
### 4:1 MUX Data flow Modelling- Testbench
```verilog
// Testbench Skeleton
`timescale 1ns/1ps
module tb_mux4_dataflow;

    // Declare testbench signals
    reg I0, I1, I2, I3;
    reg S0, S1;
    wire Y;

    // Instantiate DUT
    mux4_dataflow uut (
        .I0(I0), .I1(I1), .I2(I2), .I3(I3),
        .S0(S0), .S1(S1),
        .Y(Y)
    );

    initial begin
        // Initialize inputs

        // Apply test cases

        // Stop simulation
        #10 $stop;
    end

endmodule

```
## Simulated Output Dataflow Modelling

<img width="1349" height="757" alt="Data" src="https://github.com/user-attachments/assets/e902864c-dea8-4634-91c3-b562dcf9a64d" />

---
### 4:1 MUX Behavioral Implementation
```verilog
module mux4_to_1_behavioral (
    input wire A,
    input wire B,
    input wire C,
    input wire D,
    input wire S0,
    input wire S1,
    output reg Y
);
    always @(*) begin
        
    end
endmodule
```
### 4:1 MUX Behavioral Modelling- Testbench
```verilog
// Testbench Skeleton
`timescale 1ns/1ps
module tb_mux4_behavioral;

    // Declare testbench signals
    reg I0, I1, I2, I3;
    reg S0, S1;
    wire Y;

    // Instantiate DUT
    mux4_behavioral uut (
        .I0(I0), .I1(I1), .I2(I2), .I3(I3),
        .S0(S0), .S1(S1),
        .Y(Y)
    );

    initial begin
        // Initialize inputs

        // Apply test cases

        // Stop simulation
        #10 $stop;
    end

endmodule

```
## Simulated Output Behavioral Modelling

<img width="1348" height="757" alt="image" src="https://github.com/user-attachments/assets/1d043582-654d-423b-abf8-aa3610230d41" />



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




endmodule
```
### Testbench Implementation
```verilog
`timescale 1ns / 1ps

module mux4_to_1_tb;
    reg A, B, C, D, S0, S1;
    wire Y_gate, Y_dataflow, Y_behavioral, Y_structural;

    

    initial begin
        A = 0; B = 0; C = 0; D = 0; S0 = 0; S1 = 0;

      
        #10 $stop;
    end

   
    end
endmodule
```
## Simulated Output Structural Modelling
<img width="1351" height="758" alt="Structural" src="https://github.com/user-attachments/assets/f69e6842-56c5-497a-8564-4d06fcab7264" />



---
### CONCLUSION

In this experiment, a 4:1 Multiplexer was successfully designed and simulated using Verilog HDL across four different modeling styles: Gate-Level, Data Flow, Behavioral, and Structural.The simulation results verified the correct functionality of the MUX, with all implementations producing identical outputs for the given input conditions.

