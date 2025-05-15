# 32Bit-ALU_Synthesis

## Aim:

Synthesize 32 Bit ALU design using Constraints and analyse area and Power reports.

## Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

Synthesis: Genus

### Step 1: Getting Started

Synthesis requires three files as follows,

◦ Liberty Files (.lib)

![Screenshot 2025-04-22 181212](https://github.com/user-attachments/assets/6e5dd622-900f-47c3-81ef-2b370707db70)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

**Design Code**

module ALU (
    input  [3:0] A, B,
    input  [2:0] ALU_Sel,
    output reg [3:0] ALU_Out,
    output reg CarryOut
);

    always @(*) begin
        case (ALU_Sel)
            3'b000: {CarryOut, ALU_Out} = A + B;
            3'b001: {CarryOut, ALU_Out} = A - B;
            3'b010: ALU_Out = A & B;
            3'b011: ALU_Out = A | B;
            3'b100: ALU_Out = A ^ B;
            3'b101: ALU_Out = ~A;
            3'b110: ALU_Out = A << 1;
            3'b111: ALU_Out = A >> 1;
            default: ALU_Out = 4'b0000;
        endcase
    end
endmodule

**TestBench:**

module ALU_tb;
    reg [3:0] A, B;
    reg [2:0] ALU_Sel;
    wire [3:0] ALU_Out;
    wire CarryOut;

    ALU uut (
        .A(A),
        .B(B),
        .ALU_Sel(ALU_Sel),
        .ALU_Out(ALU_Out),
        .CarryOut(CarryOut)
    );

    initial begin
        A = 4'b0101; B = 4'b0011; ALU_Sel = 3'b000; #10;
        A = 4'b0101; B = 4'b0011; ALU_Sel = 3'b001; #10;
        A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b010; #10;
        A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b011; #10;
        A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b100; #10;
        A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b101; #10;
        A = 4'b0011; B = 4'b0000; ALU_Sel = 3'b110; #10;
        A = 4'b0011; B = 4'b0000; ALU_Sel = 3'b111; #10;
        $finish;
    end
endmodule


### Step 2 : Performing Synthesis

The Liberty files are present in the library path,

![Screenshot 2025-05-15 180504](https://github.com/user-attachments/assets/aceb5b03-18b5-41e7-9360-b36b1a06200a)


• The Available technology nodes are 180nm ,90nm and 45nm.

• In the terminal, initialise the tools with the following commands if a new terminal is being
used.

◦ csh

![Screenshot 2025-04-22 181212](https://github.com/user-attachments/assets/48ff614f-3f23-4a40-8e44-52e371f82953)

◦ source /cadence/install/cshrc

![Screenshot 2025-05-15 183111](https://github.com/user-attachments/assets/b3424208-95f5-4950-bc71-c9e967928d33)

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

![Screenshot 2025-05-15 181245](https://github.com/user-attachments/assets/96c38ddd-6228-4ec2-a206-5d9fca0b13e9)


• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist.

#### Synthesis RTL Schematic :

![Screenshot 2025-04-25 173137](https://github.com/user-attachments/assets/ebf69a2a-a9d3-4480-94e4-ae179ede563e)


#### Area report:

![Screenshot 2025-05-15 181153](https://github.com/user-attachments/assets/dfad60a5-ac01-4d4d-9d05-498ccea2cff9)


#### Power Report:

![Screenshot 2025-05-15 180714](https://github.com/user-attachments/assets/c3bc3f33-0477-4448-87a5-0849f097373e)


#### Result: 

![Screenshot 2025-05-02 174025](https://github.com/user-attachments/assets/f8fdf1bc-6a60-4037-98f7-ce5fba4ce1d8)


The generic netlist of 32 bit ALU  has been created, and area, power reports have been tabulated and generated using Genus.
