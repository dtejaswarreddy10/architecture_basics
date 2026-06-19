# NPU — Neural Processing Unit

> **Essence:** A chip purpose-built for neural-network math — running AI inference fast and at very low power, especially on phones and edge devices.

---

## 1. Introduction

### What is an NPU?
An **NPU (Neural Processing Unit)** is a processor **specialized for artificial-intelligence math** — specifically the operations inside neural networks: **matrix multiplications, convolutions, and activations**.

- A **CPU** is a general thinker; a **GPU** is a parallel number-cruncher…
- An **NPU** is a **dedicated AI engine** — it does *one family* of math (neural networks) extremely fast and extremely efficiently.

### Where did NPUs come from?
NPUs appeared because **AI moved onto everyday devices**:

- Phones needed **face unlock, photo enhancement, voice assistants** — *instantly* and *without draining the battery*.
- Running AI on a CPU was too slow; on a GPU it used too much power.
- So vendors added a **small, efficient AI block** directly into the chip (SoC).

The result: AI that runs **on-device**, privately, with tiny power budgets.

### The main idea behind NPU design
> **Do neural-network math with maximum performance-per-watt.**

Instead of being general, an NPU hard-wires the exact operations AI needs (multiply-accumulate at massive scale) and uses **low-precision numbers** to save power and area.

---

## 2. Basic Functionality & Architecture

### Simple analogy: a dedicated AI assembly line
A GPU is a general factory. An NPU is a **purpose-built assembly line** that only makes one product — neural-network results — so every part of it is tuned for that single job.

### The core building block: MAC arrays
Neural networks are mostly **multiply-and-accumulate (MAC)** operations:

$$ \text{output} = \sum_{i} (w_i \times x_i) $$

An NPU contains **huge arrays of MAC units** that perform thousands of these every cycle, plus dedicated hardware for **convolution** and **activation functions** (ReLU, etc.).

### Low precision = efficiency
NPUs rarely use full 32-bit math. AI tolerates lower precision, so they use:

| Precision | Use |
|-----------|-----|
| **INT8** | Most inference — small, fast, low power |
| **FP16 / BF16** | Higher-accuracy inference / light training |
| **INT4 / FP8** | Cutting-edge, ultra-efficient inference |

Lower precision → **more operations per watt** and **smaller chips**.

### Dataflow & on-chip memory
- NPUs keep **weights and activations in local SRAM** to avoid slow trips to main memory.
- A **dataflow design** streams data through the MAC array, maximizing reuse and minimizing energy.
- Performance is measured in **TOPS** (Tera-Operations Per Second), often with a **TOPS/Watt** efficiency figure.

### NPU vs GPU vs CPU

| Feature | CPU | GPU | NPU |
|---------|-----|-----|-----|
| Specialization | General | Parallel math | **AI only** |
| Power efficiency | Low | Medium | **Very high** |
| Best precision | FP32/64 | FP16–FP32 | **INT8 / FP16** |
| Typical home | Everywhere | PC / data center | **Phones / edge / SoC** |
| Flexibility | Highest | High | **Low (AI-focused)** |

---

## 3. Applications

### On-device / edge AI (the sweet spot)
NPUs shine where AI must run **locally, instantly, and at low power**:

- 📷 **Computational photography** — night mode, portrait blur, super-resolution
- 🗣️ **Voice assistants & speech-to-text**
- 🔐 **Face unlock & biometrics**
- 🌐 **Live translation & transcription**
- 🤖 **On-device generative AI** (small LLMs, image generation)

### Why on-device AI matters
- **Privacy** — data never leaves the device
- **Latency** — no round-trip to the cloud
- **Battery** — far more efficient than CPU/GPU for AI
- **Offline** — works without a network

### What NPUs are NOT good at
- General-purpose programs → **CPU**
- Graphics and broad parallel compute → **GPU**
- Large-scale AI *training* in data centers → **GPU/TPU**
- Anything that isn't neural-network-shaped math

---

## 4. Market Examples & Future

### Where NPUs live today
| Vendor | NPU / engine | Found in |
|--------|--------------|----------|
| **Apple** | Neural Engine | iPhone, iPad, Mac (M-series) |
| **Qualcomm** | Hexagon NPU | Snapdragon phones & PCs |
| **Google** | Tensor (Edge TPU) | Pixel phones |
| **Samsung** | Exynos NPU | Galaxy devices |
| **ARM** | Ethos NPU (licensed IP) | Many SoCs |
| **Intel / AMD** | NPU in Core / Ryzen AI | "AI PC" laptops |

### The "AI PC" wave
NPUs are now standard in laptops (Microsoft's **Copilot+ PCs** require an NPU), bringing on-device AI to mainstream computing — typically **40+ TOPS**.

### Trends
- **Rising TOPS** — tens to hundreds, on-device
- **Generative AI on the edge** — local LLMs and image models
- **Lower precision** — INT4/FP8 for more efficiency
- **NPUs everywhere** — phones, PCs, cars, wearables, IoT

---

## 5. Summary

### NPU in one paragraph
An NPU is a processor **purpose-built for neural-network math**. It packs large arrays of multiply-accumulate units and low-precision arithmetic to run AI **inference** with the best possible **performance-per-watt**. By specializing, it gives up general flexibility but enables fast, private, battery-friendly AI directly on phones, PCs, and edge devices.

### When should you choose an NPU?
**An NPU is the right tool when:**
- You run **AI inference on-device** (phone, laptop, edge)
- **Power efficiency and battery life** matter
- You need **low latency** and **privacy** (no cloud)

**Use a GPU/TPU instead for** large-scale AI *training* in the data center, and a **CPU** for general logic.

### Future trends
- On-device generative AI becoming normal
- Hundreds of TOPS in consumer chips
- Ultra-low-precision math (INT4, FP8)
- NPUs as a standard SoC block alongside CPU + GPU

> The NPU is turning every phone and laptop into a small, private **AI computer**.
