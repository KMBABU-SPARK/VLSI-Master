# 📘 RISC-V Instruction Formats – Lecture 28 Summary

This document summarizes the **RISC-V Instruction Formats** as discussed in Lecture 28 (Part 3). It is meant for learners of **Digital Design and Computer Architecture with Verilog**.

---

## 🧠 What Are Instruction Formats?

In a computer system:

- Everything (including instructions) is stored in **binary**.
- These instructions are called **machine code**.
- RISC-V uses a **fixed 32-bit instruction** size.
- Each 32-bit instruction is broken into fields such as **opcode**, **registers**, **immediate values**, etc.

> **RISC-V supports 6 standard instruction formats**:
`R`, `I`, `S`, `SB`, `U`, and `UJ`

---

## 🔹 R-Format (Register Format)

Used for: `add`, `sub`, `and`, `or`, `sll`, etc.

### Structure:

| Field     | Bits   | Description                      |
|-----------|--------|----------------------------------|
| funct7    | 7 bits | Additional function specifier    |
| rs2       | 5 bits | Second source register           |
| rs1       | 5 bits | First source register            |
| funct3    | 3 bits | Function code                    |
| rd        | 5 bits | Destination register             |
| opcode    | 7 bits | Operation type                   |

### Example:

```assembly
add x9, x20, x21
Binary: 0000000_10101_10100_000_01001_0110011
Hex   : 0x015A04B3
