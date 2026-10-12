# Integrated Circuit Blocks — Design & Verification Matrix

This document provides a concise reference matrix detailing all standard cells and full-custom macro circuits developed in Cadence Virtuoso, along with their verification statuses.

---

## 1. Standard Cell Library Summary

| Cell Identifier | Function / Equation | Inputs | Outputs | Primary Application | Pre-Sim Status |
| :--- | :--- | :---: | :---: | :--- | :---: |
| **OR2** | $Y = A + B$ | 2 | 1 | Basic Logic / CLA Carry terms | Verified |
| **OR3** | $Y = A + B + C$ | 3 | 1 | CLA Stage 2 Carry ($C_2$) | Verified |
| **OR4** | $Y = A + B + C + D$ | 4 | 1 | CLA Stage 3 Carry ($C_3$) | Verified |
| **OR5** | $Y = A + B + C + D + E$ | 5 | 1 | CLA Stage 4 Carry ($C_4$) | Verified |
| **AND2** | $Y = A \cdot B$ | 2 | 1 | CLA Generate term $G_i = A_i \cdot B_i$ | Verified |
| **AND3** | $Y = A \cdot B \cdot C$ | 3 | 1 | CLA Carry lookahead term $P_1 P_0 C_0$ | Verified |
| **AND4** | $Y = A \cdot B \cdot C \cdot D$ | 4 | 1 | CLA Carry lookahead term $P_2 P_1 P_0 C_0$ | Verified |
| **AND5** | $Y = A \cdot B \cdot C \cdot D \cdot E$ | 5 | 1 | CLA Carry lookahead term $P_3 P_2 P_1 P_0 C_0$ | Verified |
| **XOR3** | $Y = A \oplus B \oplus C$ | 3 | 1 | CLA Bit Sum generation $S_i = A_i \oplus B_i \oplus C_i$ | Verified |

---

## 2. Full-Custom Macro Circuits Summary

| Macro Name | Architecture | Input Signals | Output Signals | Layout View | DRC Status | LVS Status | Post-Layout Sim |
| :--- | :--- | :--- | :--- | :---: | :---: | :---: | :---: |
| **D-Latch** | Level-sensitive CMOS Transmission Gate / Inverter loop | `D`, `CLK` / `EN` | `Q`, `Q_bar` | Full-Custom | 0 Violations | Clean Match | Verified |
| **Master-Slave D Flip-Flop** | Edge-triggered cascaded master & slave latch cells | `D`, `CLK` | `Q` | Full-Custom | 0 Violations | Clean Match | Verified |
| **4-Bit Parallel Register** | 4-bit synchronous bus storage array | `D[3:0]`, `CLK` | `Q[3:0]` | Abutted Multi-bit Array | 0 Violations | Clean Match | Verified |
| **8-Bit Synchronous Counter** | 8-stage synchronous binary counting logic | `CLK`, `RST` | `Q[7:0]` (8-bit bus) | High-Density Matrix | 0 Violations | Clean Match | Verified |
| **4-Bit Carry Look-Ahead Adder (CLA)** | Parallel Carry Lookahead Logic ($G_i, P_i, C_i$) | `A[3:0]`, `B[3:0]`, `Cin` | `S[3:0]`, `Cout` | Standard-cell Hierarchical Layout | 0 Violations | Clean Match | Verified |

---

## 3. Key Design Verification Highlights

1. **DRC Compliance:** All layout cells adhere to foundry geometric spacing, min-width, well-tap proximity, and metallization design rules.
2. **LVS Equivalence:** Transistor-level schematic netlists correspond exactly to the extracted layout netlists across pins, terminals, and device topologies.
3. **Post-Layout Validation:** Parasitic effects extracted via PEX confirm proper signal integrity, clean switching edges, and preserved digital noise margins.
