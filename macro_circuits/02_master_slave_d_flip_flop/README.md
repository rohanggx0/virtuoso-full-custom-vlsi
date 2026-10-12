# Master-Slave D Flip-Flop (Edge-Triggered)

## 1. Executive Summary
The **Master-Slave D Flip-Flop (DFF)** is a sequential storage cell designed in **Cadence Virtuoso** to provide positive edge-triggered data sampling. By cascading two opposite-phase D-Latches (a negative-transparent **Master Latch** followed by a positive-transparent **Slave Latch**), race-around conditions and transparency hazards are eliminated.

This cell forms the atomic synchronous memory unit for the higher-level sequential macros: the **4-Bit Parallel Register** and the **8-Bit Synchronous Counter**.

---

## 2. Master-Slave Architecture & Timing

```mermaid
flowchart LR
    D[Data In D] --> Master[Master Latch<br/>Transparent when CLK=0]
    CLK[Clock CLK] --> Inv[Inverter]
    Inv --> Master
    CLK --> Slave
    Master --> QM[Internal Node Q_m]
    QM --> Slave[Slave Latch<br/>Transparent when CLK=1]
    Slave --> Q[Output Q]
```

* **When `CLK = 0`:** Master latch is transparent and samples $D$; Slave latch is opaque and holds the previous output $Q$.
* **When `CLK` transitions $0 \to 1$ (Rising Edge):** Master latch latches $D$ and becomes opaque; Slave latch turns transparent and drives the latched data to output $Q$.
* **When `CLK = 1`:** Any further transitions on $D$ are blocked by the opaque Master latch, ensuring edge-triggered behavior.

---

## 3. Schematic & Symbol View

| Transistor-Level Schematic | Symbol View |
| :---: | :---: |
| ![DFF Schematic](assets/dff_schematic.png) | ![DFF Symbol](assets/dff_symbol.png) |

---

## 4. Testbench & Pre-Layout Simulation

The flip-flop was validated in Spectre by driving clock and data signals with varying edge alignments to assess setup ($t_{su}$) and hold ($t_h$) timing.

| Testbench Circuit | Pre-Layout Transient Simulation Waveform |
| :---: | :---: |
| ![DFF Testbench](assets/dff_testbench.png) | ![DFF Pre-Sim](assets/dff_pre_sim_waveform.jpeg) |

---

## 5. Physical Layout & DRC / LVS Verification

The physical layout was designed in Virtuoso Layout Suite with careful matching of clock inverter routing paths to minimize internal clock skew between Master and Slave transmission gates.

| Physical Mask Layout | DRC & LVS Clean Verification |
| :---: | :---: |
| ![DFF Layout](assets/dff_layout.png) | ![DFF DRC/LVS](assets/dff_drc_lvs.png) |

* **DRC Status:** Clean (0 violations).
* **LVS Status:** Complete match across all extracted MOS instances, ports, and interconnections.

---

## 6. Post-Layout Simulation & Waveform Analysis

| Post-Layout Extracted Waveform |
| :---: |
| ![DFF Post-Sim](assets/dff_post_sim_waveform.png) |

### Key Observations:
* **Edge-Triggered Integrity:** Output $Q$ updates strictly at rising clock edges without glitching during transparent periods.
* **Clock-to-Q Delay ($t_{C-Q}$):** Post-layout parasitics introduce a modest increase in delay, well within standard CMOS digital operating margins.
