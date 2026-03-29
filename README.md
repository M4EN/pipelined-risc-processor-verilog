# 32-bit Pipelined RISC Processor (SystemVerilog)

Design and verification of a 32-bit pipelined RISC processor implemented in SystemVerilog.  
This project implements a full 5-stage pipeline with hazard detection, forwarding, and stalling, and supports execution of complete programs through simulation.

---

## Overview

- 5-stage pipeline: IF, ID, EX, MEM, WB  
- 16 general-purpose 32-bit registers (R0–R15)  
- R15 used as Program Counter (PC), R14 as return address register  
- Separate instruction and data memory (word-addressable)  
- Custom ISA with arithmetic, logical, memory, and control-flow instructions  
- Supports full program execution (not limited to single instructions)  
- Verified using simulation-based testbenches  

---

## Architecture

### Pipeline Stages
- **IF (Instruction Fetch)** – Fetch instruction using PC  
- **ID (Instruction Decode)** – Decode instruction, read registers, generate control signals  
- **EX (Execute)** – Perform ALU operations and evaluate branches  
- **MEM (Memory Access)** – Access data memory for load/store  
- **WB (Write Back)** – Write results back to register file  

Pipeline registers are inserted between stages to enable parallel execution and improve throughput.

---

## Instruction Set (ISA)

### Arithmetic & Logical
- ADD, SUB, ADDI, CMP  
- OR, ORI  

### Memory Operations
- LW, SW  
- LDW, SDW (multi-cycle double-word operations)

### Control Flow
- BZ, BGZ, BLZ (conditional branches)  
- J, JR (jumps)  
- CALL (function call with return address stored in R14)

---

## Hazard Handling

The processor includes mechanisms to ensure correct execution in a pipelined environment:

### Data Hazards
- Forwarding (EX/MEM/WB bypassing)
- Stall insertion for load-use hazards  

### Control Hazards
- Branch and jump handling  
- Pipeline flushing using control signals  

### Structural Hazards
- Managed through pipeline control and stall logic  

---

## Forwarding and Stalling

- Forwarding unit resolves RAW dependencies without waiting for write-back  
- Stall logic inserts pipeline bubbles when data is not yet available  
- Ensures correctness while maintaining pipeline efficiency  

---

## Verification

Verification was performed using simulation-based testing:

- Custom Verilog testbench  
- Multiple assembly test programs covering all instructions  
- Cycle-by-cycle validation of register values and memory behavior  
- Waveform analysis for debugging and correctness  

### Results
- Correct execution for all core instructions  
- Hazard detection and resolution verified  
- Pipeline operates correctly across full programs  
- LDW/SDW implemented with partial limitations  

---

## Report

The repository includes a detailed report:  
**Pipelined_RISC_Processor_Report.pdf**

It covers:
- Processor architecture and datapath design  
- Instruction set and control logic  
- Pipeline implementation details  
- Hazard detection and handling  
- Verification methodology and test cases  

---

## Authors

**Maen Foqaha**  
[m4en](https://github.com/m4en)

**Samir Ali**  
[sameer5504](https://github.com/sameer5504)

**Ibrahim Al Ardah**  
[ibrahimardah](https://github.com/ibrahimardah)

---
