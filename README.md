# Sap1-CPU-in-PLC-Simulation-GX-Works3-
SAP1 Cpu simulation on PLC

<img width="467" height="562" alt="Ekran görüntüsü 2026-02-14 143216" src="https://github.com/user-attachments/assets/392da0bf-5a58-47f6-9c65-1b377633b1b4" />

Sap1 is designed for educational purposes. I created a simulation on PLC (Mitsubishi Electrix GXWorks3).You can See the fundemantal SAP1 Cpu Architecture.

<img width="2278" height="374" alt="Ekran görüntüsü 2026-02-14 143110" src="https://github.com/user-attachments/assets/636d57b0-857a-4a2c-a3ca-4006940dcf69" />
<img width="2205" height="1034" alt="Ekran görüntüsü 2026-02-14 143121" src="https://github.com/user-attachments/assets/8cc69e92-0812-4e54-9e13-43ca9928ee5b" />

Cpu Instructions processing in 6 T states. First 3 T states are common in all instructions.

T1 State: Load Program Counter Value To MAR Register(Mar selects Ram adrees)

T2 State: Increase Program Counter for next instruction.

T3 State: Load pointed Ram value to Instruction Register(ınstruction Register decode Instruction and adress)

T4 State(common for LDA,ADD,SUB): Decoded Instruction load to control matrix.Decoded Adress Load the Mar(Ram goes to pointed adress)

<img width="1889" height="605" alt="Ekran görüntüsü 2026-02-14 143237" src="https://github.com/user-attachments/assets/235c5631-13e6-402c-85ea-6e0111baaaa0" />

LDA Instruction:
  This instruction Load Value To Accumulator Register.
  <img width="1911" height="622" alt="Ekran görüntüsü 2026-02-14 143246" src="https://github.com/user-attachments/assets/42bfd495-6391-4ed8-b501-e280698dbd4c" />
  T5 State:Load pointed Ram adress to Accumulator Register.
  
ADD Instruction:
  This instruction Load Value To B Register.After that Adder calculate (A+B) value.Calculated value Stored Accumulator Register.
  T5 State:Load pointed Ram adress to B Register.

SUB Instruction:
  This instruction Load Value To B Register.After that calculate (A-B) value.Calculated value Stored Accumulator Register.
  T5 State:Load pointed Ram adress to B Register.
  
<img width="2135" height="1232" alt="Ekran görüntüsü 2026-02-14 143325" src="https://github.com/user-attachments/assets/db7728ae-97ce-4cb8-96e5-d2db5e013563" />


OUT Instruction:
  This instruciton Load Acumulator value to Output Register.
<img width="536" height="481" alt="Ekran görüntüsü 2026-02-14 145642" src="https://github.com/user-attachments/assets/1631f86c-0200-4f34-b2ff-a0717b25c4fa" />

HLT Instruction:
  This instruction Stops the Cpu Clock.
  
Every T state have different control signal: Check the case on simulated program.

More Details About SAP1 CPU: Digital Computer Electronics-Third Edition-Albert Paul Malvino,Jerald A. Brown/Page-140

