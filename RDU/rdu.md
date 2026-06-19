# RDU — Reconfigurable Dataflow Unit (SambaNova)

> **Essence:** A chip that *reshapes itself* to match your AI model. Instead of forcing the model through fixed cores, the RDU configures its hardware into the exact **dataflow** the model needs.

---

## 1. Introduction

### What is an RDU?
An **RDU (Reconfigurable Dataflow Unit)** is an AI processor from **SambaNova Systems** built on a **Reconfigurable Dataflow Architecture (RDA)**. Rather than running instructions on fixed cores (like a CPU/GPU), the RDU **rewires its compute and memory units** to form a custom pipeline that mirrors the model's **dataflow graph**.

- A **GPU** moves data in and out of fixed cores, over and over.
- An **RDU** lays the model out **spatially** and lets data **flow through** it.

### Where did RDUs come from?
SambaNova (founded 2017 by Stanford professors and ex-Sun/Oracle chip leaders) noted that AI models are **dataflow graphs**, but GPUs execute them as a long series of kernel launches with constant memory traffic. The RDU was built to **map the whole graph onto hardware** and keep data moving — reducing overhead and handling **very large models**.

### The main idea behind RDU design
> **Configure the hardware to the model, not the model to the hardware.**

The RDU is **reconfigurable**: a compiler arranges its units into the precise pipeline a model needs, so intermediate results **stream between stages on-chip** instead of bouncing to memory.

---

## 2. Basic Functionality & Architecture

### Simple analogy: a custom factory line per product
A GPU is a general workshop where every part is carried back and forth to the same machines. The RDU **builds a dedicated assembly line** shaped like your model — each station feeds the next, so the product flows straight through.

### The building blocks (RDA)
| Unit | Role |
|------|------|
| **PCUs — Pattern Compute Units** | Reconfigurable compute (matrix/vector math) |
| **PMUs — Pattern Memory Units** | Distributed on-chip memory near compute |
| **Switching fabric** | Programmable interconnect linking PCUs &amp; PMUs |
| **Compiler (SambaFlow)** | Maps the model's dataflow graph onto the fabric |

### Spatial dataflow vs instruction streams
- A GPU executes a **stream of instructions/kernels**, repeatedly reading & writing memory.
- The RDU is **configured once** into a spatial pipeline; data then **flows** through PCUs and PMUs with minimal memory round-trips.
- This reduces **overhead** and keeps units busy.

### Built for big models
SambaNova emphasizes a **three-tier memory** system (including large amounts of memory per system) so a single RDU system can hold **very large models** (hundreds of billions of parameters) and **long context** without splitting across as many devices.

### RDU vs GPU

| Feature | GPU | RDU |
|---------|-----|-----|
| Execution | Instruction/kernel streams | **Spatial dataflow** |
| Adapts to model | Fixed cores | **Reconfigures to the graph** |
| Memory traffic | High (constant round-trips) | **Lower — on-chip streaming** |
| Big-model focus | Split across many GPUs | **Large models on fewer chips** |
| Software | CUDA | **SambaFlow** |

---

## 3. Applications

### Where RDUs fit
- 🧠 **Large language models** — training &amp; inference
- 📚 **Long-context** &amp; large-parameter models
- 🏢 **Enterprise &amp; government AI** — delivered as full systems
- 🔀 **Composition of Experts** — many models served efficiently
- 🔬 **Scientific / regulated** deployments (on-prem)

### Why pick an RDU?
- **Big models on fewer chips** (large memory capacity)
- **Less memory overhead** via spatial dataflow
- **Flexible** — reconfigures per model
- Delivered as a **turnkey enterprise system**

### What RDUs are NOT for
- General-purpose computing → **CPU**
- Graphics → **GPU**
- The broadest open ecosystem (CUDA dominates)
- Tiny edge / low-power devices → **NPU**

---

## 4. Market Examples & Future

### Products & ecosystem
| Item | Note |
|------|------|
| **SN10 / SN30 / SN40L** | Successive RDU generations |
| **DataScale systems** | Full racks delivered to customers |
| **SambaNova Suite** | Enterprise AI platform (models + hardware) |
| **SambaFlow** | The dataflow compiler / software stack |

### Business context
SambaNova sells **complete AI systems** (hardware + models + software) rather than just chips, targeting **enterprises and governments** that want large models run **on-premise**. The **SN40L** highlights big on-package memory to serve very large models efficiently.

### Trends
- **Memory capacity** as a differentiator for huge models
- **Composition of Experts** — many specialized models, served together
- Enterprise/on-prem AI appliances
- Dataflow as an alternative to instruction-stream GPUs

---

## 5. Summary

### RDU in one paragraph
The RDU is SambaNova's AI processor built on a **Reconfigurable Dataflow Architecture**: a compiler arranges its Pattern Compute Units and Pattern Memory Units into a **spatial pipeline shaped like the model's dataflow graph**, so data streams between stages on-chip with little memory overhead. With large memory capacity, it runs **very large models on fewer chips** and is delivered as turnkey enterprise systems — distinct from the GPU's instruction-stream model.

### When should you choose an RDU?
**An RDU makes sense when:**
- You run **very large models** / long context
- You want **big models on fewer chips**
- You prefer a **turnkey enterprise/on-prem system**
- You benefit from **dataflow** efficiency

**Use a GPU** for the broadest ecosystem and flexible workloads.

### Future trends
- Large on-package memory for frontier models
- Composition-of-Experts serving
- Enterprise &amp; sovereign AI appliances
- Dataflow architectures maturing

> The RDU's idea: don't squeeze the model into the chip — **reshape the chip into the model**.
