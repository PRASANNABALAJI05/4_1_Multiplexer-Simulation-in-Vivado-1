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
module MUX4_1_GATE (
    input  wire [3:0] I,   
    input  wire [1:0] S,   
    output wire Y         
);
    wire w1, w2, w3, w4;

    // AND gates with ~ usage
    and g1(w1, I[0], ~S[0], ~S[1]); // Select I0
    and g2(w2, I[1], ~S[0],  S[1]); // Select I1
    and g3(w3, I[2],  S[0], ~S[1]); // Select I2
    and g4(w4, I[3],  S[0],  S[1]); // Select I3

    // OR gate
    or g5(Y, w1, w2, w3, w4);
endmodule
```
### 4:1 MUX Gate-Level Implementation- Testbench
```verilog
`timescale 1ns / 1ps
module tb_MUX4_1_GATE;
    reg [3:0] I;
    reg [1:0] S;
    wire Y;

    // Instantiate DUT
    MUX4_1_GATE uut (.I(I), .S(S), .Y(Y));

    initial begin
        $monitor("Time=%0t | I=%b | S=%b | Y=%b", $time, I, S, Y);

        I = 4'b1010;
        S = 2'b00; #10;
        S = 2'b01; #10;
        S = 2'b10; #10;
        S = 2'b11; #10;

        I = 4'b0010;
        S = 2'b00; #10;
        S = 2'b01; #10;
        S = 2'b10; #10;
        S = 2'b11; #10;

        $finish;
    end
endmodule
```
## Simulated Output Gate Level Modelling

<img width="1919" height="1079" alt="GATE (2)" src="https://github.com/user-attachments/assets/7f3fae93-da69-4360-8a0b-1813641dc7ae" />

---
### 4:1 MUX Data flow Modelling
```verilog
module mux4_dataflow (
    input  wire I0, I1, I2, I3,
    input  wire S0, S1,
    output wire Y
);
    wire [4:1] w;

    assign w[1] = I0 & ~S1 & ~S0; // S=00 → I0
    assign w[2] = I1 & ~S1 &  S0; // S=01 → I1
    assign w[3] = I2 &  S1 & ~S0; // S=10 → I2
    assign w[4] = I3 &  S1 &  S0; // S=11 → I3

    assign Y = w[1] | w[2] | w[3] | w[4];
endmodule
 

```
### 4:1 MUX Data flow Modelling- Testbench
```verilog
`timescale 1ns/1ps
module MUX4_1_DATA_tb;
reg [3:0]I;
reg [1:0]S;
wire Y;
MUX4_1_DATA uut(I,S,Y);
initial
begin
I=4'B0001;
S=2'b00;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b01;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b10;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b11;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
$finish;
end 
endmodule

```
## Simulated Output Dataflow Modelling

<img width="1919" height="1079" alt="DATA (2)" src="https://github.com/user-attachments/assets/fba7f396-83f2-4e42-9b3b-d243e5a65bba" />

---
### 4:1 MUX Behavioral Implementation
```verilog
module MUX4_1_BEHAVIOURAL(I,S,Y);
input [3:0]I;
input[1:0]S;
output reg Y;
always @(I,S)
begin
case(S)
2'b00:Y=I[0];
2'b01:Y=I[1];
2'b10:Y=I[2];
2'b11:Y=I[3];
endcase
end
endmodule
```
### 4:1 MUX Behavioral Modelling- Testbench
```verilog
`timescale 1ns/1ps
module MUX4_1_BEHAVIOURAL_tb;
reg [3:0]I;
reg [1:0]S;
wire Y;
MUX4_1_BEHAVIOURAL uut(I,S,Y);
initial
begin
I=4'B1001;
S=2'b00;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b01;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b10;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b11;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
$finish;
end
endmodule

```
## Simulated Output Behavioral Modelling
<img width="1919" height="1079" alt="BEHAVIOURAL" src="https://github.com/user-attachments/assets/8159e8fb-5c89-4ff4-8ff1-c885b8f9406b" />



### 4:1 MUX Structural Implementation

![image](https://github.com/user-attachments/assets/eea81c2c-7dfa-43aa-9cea-1ab4ed54db6c)


```verilog
module MUX21(A,B,S,Z);
input A,B,S;
output Z;
wire W1,W2;
and g1(W1,A,~S);
and g2(W2,B,S);
or g3(Z,W1,W2);
endmodule

module MUX4_1_STRUCTURAL(I,S,Y);
input [3:0]I;
input [1:0]S;
output Y;
wire [2:1]W;
MUX21 M1(.Z(W[1]),.A(I[0]),.B(I[1]),.S(S[1]));
MUX21 M2(.Z(W[2]),.A(I[2]),.B(I[3]),.S(S[1]));
MUX21 M3(.Z(Y),.A(W[1]),.B(W[2]),.S(S[0]));
endmodule

```
### Testbench Implementation
```verilog
 `timescale 1ns / 1ps
module MUX4_1_STRUCTURAL_tb;
reg [3:0]I;
reg [1:0]S;
wire Y;
MUX4_1_STRUCTURAL uut(I,S,Y);
initial
begin
I=4'B1000;
S=2'b00;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b01;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b10;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
S=2'b11;
#10
$display("Selection is %b %b , output : %b ", S[1],S[0],Y);
$finish;
end
endmodule
```
## Simulated Output Structural Modelling

<img width="1919" height="1079" alt="STRUCTURL" src="https://github.com/user-attachments/assets/014a04b4-5e8b-44d0-8309-8b8ab5886a82" />

---
### CONCLUSION

In this experiment, a 4:1 Multiplexer was successfully designed and simulated using Verilog HDL across four different modeling styles: Gate-Level, Data Flow, Behavioral, and Structural.The simulation results verified the correct functionality of the MUX, with all implementations producing identical outputs for the given input conditions.

