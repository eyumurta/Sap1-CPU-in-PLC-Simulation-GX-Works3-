🇺🇸 English | 🇹🇷 Türkçe

[English Version](README_EN.md)
[Turkish Version](README_TR.md)

# Sap1-CPU-in-PLC-Simulation-GX-Works3-
SAP1 Cpu simulation on PLC

<img width="467" height="562" alt="Ekran görüntüsü 2026-02-14 143216" src="https://github.com/user-attachments/assets/392da0bf-5a58-47f6-9c65-1b377633b1b4" />

Sap1 is designed for educational purposes. I created a simulation on PLC (Mitsubishi Electrix GXWorks3).You can See the fundemantal SAP1 Cpu Architecture.

<img width="2278" height="374" alt="Ekran görüntüsü 2026-02-14 143110" src="https://github.com/user-attachments/assets/636d57b0-857a-4a2c-a3ca-4006940dcf69" />
<img width="2205" height="1034" alt="Ekran görüntüsü 2026-02-14 143121" src="https://github.com/user-attachments/assets/8cc69e92-0812-4e54-9e13-43ca9928ee5b" />

Cpu Instructions processing in 6 T states. First 3 T states are common in all instructions.

## SAP1 Registers 

##### Program Counter:

Points to the program address in memory.
When Cp input is active, the counter increments.
When Ep input is active, the PC value is loaded onto the WBus.

##### Input and MAR:

This register indicates which address in RAM memory will be accessed.
When the Lm signal is active, the WBus value is loaded into the MAR register.

##### RAM:

The RAM stores the user program and data.
RAM memory has 16 cells, each cell is 8 bits long.
When the Ce signal is low, the RAM value is loaded onto the WBus.

##### Instruction Register:

The Instruction Register decodes the instruction code and address value.
The 4-bit MSB represents the instruction, and the 4-bit LSB represents the address.
When the Ei signal is low, the WBus value is loaded into the IR register.
When the Li signal is active, the decoded address value is loaded onto the WBus.
In my simulation, the IR value is always loaded into the control matrix.

##### Accumulator:

This register is used by the LDA instruction.
At the same time, added and subtracted values are stored here.
When the LA signal is active, the WBus value is loaded into the Accumulator register.
When the EA signal is activated, the Accumulator value is loaded onto the WBus.

##### Adder/Subtractor:

This is part of the ALU (Arithmetic Logic Unit) of the CPU.
When the Eu signal is activated, the add/sub result is loaded onto the WBus.
When the Su signal is inactive, it works in addition mode.
When the Su signal is active, it works in subtraction mode.

##### B Register:

The B register is a buffer register for ADD and SUB instructions.
When the LB signal is active, the WBus value is loaded into the B register.

##### Output Register:

This register is used by the OUT instruction.
When the Lo signal is active, the WBus value is loaded into the Output register.

## T-States

##### T1 State: 
  Load Program Counter Value To MAR Register(Mar selects Ram adrees)

##### T2 State: 
  Increase Program Counter for next instruction.

##### T3 State: 
  Load pointed Ram value to Instruction Register(ınstruction Register decode Instruction and adress)

##### T4 State(common for LDA,ADD,SUB):
   Decoded Instruction load to control matrix.Decoded Adress Load the Mar(Ram goes to pointed adress)

<img width="1889" height="605" alt="Ekran görüntüsü 2026-02-14 143237" src="https://github.com/user-attachments/assets/235c5631-13e6-402c-85ea-6e0111baaaa0" />

## Instructions

##### LDA Instruction:
  This instruction Load Value To Accumulator Register.
  <img width="1911" height="622" alt="Ekran görüntüsü 2026-02-14 143246" src="https://github.com/user-attachments/assets/42bfd495-6391-4ed8-b501-e280698dbd4c" />
  T5 State:Load pointed Ram adress to Accumulator Register.
  
##### ADD Instruction:
  This instruction Load Value To B Register.After that Adder calculate (A+B) value.Calculated value Stored Accumulator Register.
  T5 State:Load pointed Ram adress to B Register.

##### SUB Instruction:
  This instruction Load Value To B Register.After that calculate (A-B) value.Calculated value Stored Accumulator Register.
  T5 State:Load pointed Ram adress to B Register.
  
<img width="2156" height="1199" alt="Ekran görüntüsü 2026-02-15 102730" src="https://github.com/user-attachments/assets/4fae1b53-3e05-4140-a843-ee4748f59029" />


##### OUT Instruction:
  This instruciton Load Acumulator value to Output Register.
  
<img width="536" height="481" alt="Ekran görüntüsü 2026-02-14 145642" src="https://github.com/user-attachments/assets/1631f86c-0200-4f34-b2ff-a0717b25c4fa" />

##### HLT Instruction:
  This instruction Stops the Cpu Clock.
  
Every T state have different control signal: Check the case on simulated program.

More Details About SAP1 CPU: Digital Computer Electronics-Third Edition-Albert Paul Malvino,Jerald A. Brown/Page-140

