# Basic CPU Architecture 🧠🖥️

A VHDL-based CPU design project simulating a basic von Neumann-style architecture. Implemented as part of the **Computer Organization and System Programming** course at the **German University in Cairo (GUC)**, this project covers instruction decoding, control signal generation, register manipulation, and ALU operations.

---

## 📘 Project Overview

This project involves implementing a simplified CPU in VHDL, capable of executing a predefined instruction set using control units, registers, memory interface, and a basic arithmetic logic unit (ALU). The architecture follows a microprogrammed control approach with defined register-transfer-level (RTL) instructions and timing cycles.

---

## ✅ Supported Instructions

The CPU can execute the following operations:

| Mnemonic | Description               | Notes                          |
|----------|---------------------------|--------------------------------|
| `DIV`    | Divide DR by AC           | Result → AC                    |
| `ADD`    | Add DR to AC              | Result → AC, Carry → E         |
| `LDA`    | Load value to AC          | AC ← M[AR]                     |
| `STA`    | Store AC to memory        | M[AR] ← AC                     |
| `BUN`    | Branch Unconditionally    | PC ← AR                        |
| `MUL`    | Multiply DR and AC        | Result → AC                    |
| `ISZ`    | Increment and Skip if Zero| DR ← DR+1; skip next if zero   |

---

## 🧠 Micro-Operations (RTL)

Each instruction is broken into micro-operations (timing steps T0–T6) such as:

- `T0`: `AR ← PC`
- `T1`: `IR ← M[AR]; PC ← PC + 1`
- `T2`: `Decode IR; AR ← IR(0–11)`
- Execution steps: `D0T3` to `D6T5` for specific instructions

Example for `ADD`:


---

## ⚙️ Components & Control Signals

### Registers

| Register | Load Condition(s)                      |
|----------|----------------------------------------|
| AR       | `T0`, `T2`                             |
| IR       | `T1`                                   |
| DR       | `D0T3`, `D1T3`, `D2T3`, `D5T3`, `D6T3`, `D0T5` |
| TR       | `D0T4`                                 |
| PC       | `D4T3` (load), `T1` + `D6T5` (increment)|
| AC       | `D0T4`, `D1T4`, `D2T4`, `D5T4`, `D0T6`  |

### Memory

- **Read**: `T1`, `D0T3`, `D1T3`, `D2T3`, `D5T3`, `D6T3`
- **Write**: `D3T3`, `D6T5`

### Sequence Counter (SC)

- **Clear**: `D3T3`, `D4T3`, `D1T4`, `D2T4`, `D5T4`, `D6T5`, `D0T6`

### ALU Operations

| Code | Operation         |
|------|-------------------|
| `001`| Transfer A (from DR) |
| `011`| Multiply A × B     |
| `101`| Divide A ÷ B       |
| `110`| Add A + B          |

---

## 🔁 Instruction Cycle Example: `MUL`


---

## 📂 File Structure (Suggested)


---

## 🧪 Team Members

| Name                      | ID        | Email                                |
|---------------------------|-----------|--------------------------------------|
| Mohamed Yaser Ahmed       | 58-21125  | mohamed.yaseribrahim@student.guc.edu.eg |
| Ahmed Tarek El Husseini   | 58-21270  | ahmed.husseini@student.guc.edu.eg   |
| Mohamed Ibrahim Ismail    | 58-16326  | mohamed.ahmedismail@student.guc.edu.eg |
| Mohamed Mohsen Abu Ayad   | 58-1653   | mohamed.aboayad@student.guc.edu.eg  |
| Ahmed Tarek Rashad        | 58-2693   | ahmed.rashad@guc.edu.eg             |

---

## 📜 License

This project is developed for academic purposes as part of the coursework at GUC. All rights reserved to the respective contributors.

