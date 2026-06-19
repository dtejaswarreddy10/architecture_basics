# FPGA — Field-Programmable Gate Array

> **Essence:** A chip whose hardware you can *reprogram* after it's built — a blank canvas of logic blocks you wire into any digital circuit you need.

---

## 1. Introduction

### What is an FPGA?
An **FPGA (Field-Programmable Gate Array)** is a chip made of **reconfigurable hardware**. Instead of running software on a fixed processor, you **rewire the chip itself** to *become* the circuit you want — a network controller, a video processor, an AI accelerator, anything.

- A **CPU/GPU** runs instructions on *fixed* hardware.
- An **FPGA** lets you **change the hardware** to match the problem.

### Where did FPGAs come from?
FPGAs emerged in the **mid-1980s** (Xilinx shipped the first in **1985**) as a flexible middle ground between:

- **Fixed custom chips (ASICs)** — fast but expensive and unchangeable, and
- **General processors** — flexible but slower for specialized tasks.

They became essential for **prototyping** chips and for products needing custom hardware in **small volumes**.

### The main idea behind FPGA design
> **Make the hardware itself programmable.**

An FPGA provides a sea of generic logic blocks and wires. A **configuration bitstream** sets how they connect, so the same physical chip can implement *any* digital design — and be **reprogrammed** later.

---

## 2. Basic Functionality & Architecture

### Simple analogy: electronic LEGO
An FPGA is like a giant box of **electronic LEGO**. The blocks are generic, but you can snap them together into almost any shape — and if you want something different tomorrow, you **take it apart and rebuild**.

### The core building blocks
| Block | What it does |
|-------|--------------|
| **LUTs (Look-Up Tables)** | Implement any small logic function |
| **Flip-Flops / Registers** | Store bits, hold state |
| **CLBs (Configurable Logic Blocks)** | Groups of LUTs + flip-flops |
| **DSP slices** | Fast hardware multiply-accumulate (math) |
| **Block RAM (BRAM)** | On-chip memory |
| **Programmable interconnect** | The wires that link everything |
| **I/O blocks** | Talk to the outside world |

### How it gets "programmed"
You describe the circuit in a **Hardware Description Language (HDL)** — **VHDL** or **Verilog/SystemVerilog**:

1. **Write HDL** describing the logic.
2. **Synthesize** → map it to LUTs, DSPs, BRAM.
3. **Place & route** → decide where blocks go and how to wire them.
4. **Generate a bitstream** → load it into the FPGA.

The chip now *is* your circuit — running **in true parallel hardware**, not as software.

### Why FPGAs are fast
Because logic runs as **actual parallel hardware** (not sequential instructions), FPGAs give **low, predictable latency** — ideal for real-time and high-speed streaming tasks.

### FPGA vs ASIC

| Feature | FPGA | ASIC |
|---------|------|------|
| Reconfigurable | **Yes — reprogram anytime** | No — fixed forever |
| Upfront cost (NRE) | **Low** | Very high |
| Per-unit cost | Higher | **Low at volume** |
| Performance / efficiency | High | **Highest** |
| Time to market | **Fast** | Slow |
| Best for | Prototyping, low/mid volume, evolving specs | Mass production, fixed function |

---

## 3. Applications

### Where FPGAs shine
- 🔬 **Chip prototyping / emulation** — test an ASIC design before manufacturing
- 🌐 **Networking** — routers, switches, smart NICs, low-latency packet processing
- 📈 **High-frequency trading** — nanosecond-level deterministic latency
- 📡 **Telecom & 5G** — signal processing in base stations
- 🛰️ **Aerospace & defense** — radar, secure comms, reconfigurable in the field
- 🎥 **Video & broadcast** — real-time image processing
- 🤖 **Custom accelerators** — AI inference, genomics, finance

### Why pick an FPGA over a CPU/GPU?
- **Custom hardware** tailored to one task
- **Deterministic, ultra-low latency**
- **Massive fine-grained parallelism**
- **Reprogrammable** when standards or needs change

### What FPGAs are NOT good at
- Running general software / operating systems → **CPU**
- Easiest possible programming (HDL is harder than coding)
- Lowest cost at huge volumes → **ASIC**
- Peak raw throughput on dense matrix math → **GPU/TPU**

---

## 4. Market Examples & Future

### The major vendors
| Vendor | Family / note |
|--------|---------------|
| **AMD (Xilinx)** | Virtex, Kintex, Artix, Zynq, **Versal** — market leader |
| **Intel (Altera)** | Stratix, Arria, Cyclone, Agilex |
| **Lattice** | Small, low-power FPGAs for edge |
| **Microchip** | Flash-based & space-grade FPGAs |

### The big shift: SoC FPGAs & ACAPs
Modern FPGAs are now **whole systems on a chip**, combining:

- **ARM CPU cores** + FPGA fabric (e.g. **Xilinx Zynq**)
- **AI engines** + DSP + fabric (e.g. **Versal ACAP** — Adaptive Compute Acceleration Platform)

This blends software flexibility with reconfigurable hardware acceleration.

### Trends
- **FPGAs in data centers** for custom acceleration (networking, AI inference)
- **Adaptive SoCs** mixing CPUs, AI engines, and fabric
- **Higher-level design** (HLS — write in C/C++ instead of pure HDL)
- **Edge AI** on small, power-efficient FPGAs

---

## 5. Summary

### FPGA in one paragraph
An FPGA is a chip full of **reconfigurable logic blocks** that you wire into any digital circuit using an HDL. Because the design runs as **real parallel hardware**, FPGAs deliver low, predictable latency and high efficiency, while staying **reprogrammable** — a flexible middle ground between general processors and fixed ASICs. They're ideal for prototyping, networking, real-time processing, and evolving specifications.

### When should you choose an FPGA?
**An FPGA is the right tool when:**
- You need **custom hardware** but not millions of units
- **Latency must be ultra-low and deterministic**
- Your **design may change** (standards, algorithms)
- You're **prototyping a chip** before committing to an ASIC

**Use an ASIC** for mass production of a fixed function, and a **CPU/GPU** for general or software-driven work.

### Future trends
- Adaptive SoCs (CPU + AI engines + fabric)
- FPGAs as data-center accelerators
- Easier design via High-Level Synthesis
- Power-efficient FPGAs for edge AI

> The FPGA's superpower is **change** — hardware that can be rebuilt as fast as your ideas evolve.
