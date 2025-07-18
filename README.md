# Basic CPU Architecture 🧠🖥️

A Model-based CPU design project simulating a basic von Neumann-style architecture. This project covers instruction decoding, control signal generation, register manipulation, and ALU operations.

---

## 📘 Project Overview

This project involves implementing a simplified CPU on Logisim, capable of executing a predefined instruction set using control units, registers, memory interface, and a basic arithmetic logic unit (ALU). The architecture follows a microprogrammed control approach with defined register-transfer-level (RTL) instructions and timing cycles.

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

## 🧪 Team Members

| Name                      | ID        | Major                                |
|---------------------------|-----------|--------------------------------------|
| Mohamed Yaser Ahmed       | 58-21125  | Mechatronics Engineering |
| Ahmed Tarek Husseini   | 58-21270  | Mechatronics Engineering |
| Mohamed Ibrahim Ismail    | 58-16326  | Computer Science |
| Mohamed Mohsen Abu Ayad   | 58-1653   | Mechatronics Engineering |
| Ahmed Tarek Rashad        | 58-2693   | Computer Science |


