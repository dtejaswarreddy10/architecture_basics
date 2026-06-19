# Dojo — AI Training Supercomputer (Tesla)

> **Essence:** A custom supercomputer Tesla designed to train its self-driving neural networks on **enormous amounts of video**. Built from Tesla's own **D1 chip**, it scales by tiling: chips → Training Tiles → cabinets → an **ExaPOD**.

---

## 1. Introduction

### What is Dojo?
**Dojo** is a **custom AI training supercomputer** built by **Tesla** to train the vision-based neural networks behind **Full Self-Driving (FSD)** and Autopilot. Unlike most accelerators, Dojo isn't a product you can buy — it was an **internal machine**, built from Tesla's own **D1 chip**, optimized for one job: **training on video at massive scale**.

- Most chips here are sold to customers.
- **Dojo** was a **purpose-built internal supercomputer** for Tesla's own data.

### Where did Dojo come from?
Tesla collects **vast amounts of camera video** from its cars. Training vision models on that data demanded enormous compute. Rather than only buying GPUs, Tesla designed a **vertically integrated** system — its own chip, board, and interconnect — tuned specifically for **video-heavy neural-network training**.

### The main idea behind Dojo
> **Build a seamless, tileable fabric of compute optimized for one workload — training Tesla's vision networks.**

Dojo's design philosophy was to **remove boundaries between chips**, making many dies behave like one huge, uniform compute surface.

> ⚠️ **Status note (2026):** Tesla reportedly **wound down its dedicated Dojo program in 2025**, shifting toward external silicon partners and its inference-focused chips. Dojo remains an influential example of vertically integrated AI-training hardware.

---

## 2. Basic Functionality & Architecture

### Simple analogy: building with LEGO tiles
Dojo scales like **snapping LEGO tiles together**. One small block (a D1 chip) is repeated into a tile; tiles snap into cabinets; cabinets combine into a full system — each level a bigger, seamless version of the same thing.

### The scaling hierarchy
| Level | What it is |
|-------|-----------|
| **D1 chip** | Tesla's custom training die — many small cores + high on-chip bandwidth |
| **Training Tile** | **25 D1 dies** fused into one module with huge bandwidth |
| **Cabinet** | Multiple Training Tiles together |
| **ExaPOD** | Many cabinets → a full Dojo supercomputer |

### Key design ideas
- **Mesh interconnect:** D1 dies connect in a 2-D mesh so data moves between cores with very high bandwidth and low latency.
- **Seamless tiles:** the **Training Tile** packs 25 dies to act like one large chip — minimizing chip-to-chip boundaries.
- **Custom datatype (CFP8):** a configurable 8-bit float format to balance **range, precision, and efficiency** for training.
- **Bandwidth-first:** the whole stack is built to keep data flowing to compute.

### How a training run uses Dojo
1. Massive **video datasets** stream in from Tesla's fleet.
2. Work is spread across the **mesh** of D1 cores.
3. **Training Tiles** act as large seamless compute blocks.
4. **ExaPOD** scale handles the full neural-network training.

### Dojo vs a GPU cluster

| Feature | GPU cluster | Dojo |
|---------|-------------|------|
| Purpose | General AI/compute | **Tesla video training** |
| Chip | Off-the-shelf GPU | **Custom D1** |
| Scaling unit | Server + switches | **Training Tile (25 dies)** |
| Datatype | FP16/BF16/FP8 | **CFP8 (configurable)** |
| Availability | Buy/rent | **Internal to Tesla** |

---

## 3. Applications

### Where Dojo fit
- 🚗 **Autonomous-driving** vision training (FSD / Autopilot)
- 🎥 **Video-heavy** neural-network training
- 🤖 Tesla AI projects (e.g. robotics) needing huge training
- 🏭 **Vertically integrated** in-house AI compute

### Why Tesla built it
- **Tailored** to its exact training workload
- **Bandwidth** optimized for video data
- **Vertical integration** — control the whole stack
- A hedge against depending solely on external GPUs

### What Dojo is NOT
- A chip you can **buy or rent**
- General-purpose computing → **CPU**
- Graphics → **GPU**
- Edge / in-car **inference** (that's Tesla's separate FSD inference chip)

---

## 4. Market Examples & Future

### Components & system
| Item | Note |
|------|------|
| **D1 chip** | Tesla's custom 7nm-class training die |
| **Training Tile** | 25 D1 dies as one high-bandwidth module |
| **ExaPOD** | Full Dojo system of many cabinets |
| **CFP8** | Configurable 8-bit float datatype for training |

### Business context
Dojo showed how far **vertical integration** can go — a car company designing its **own AI supercomputer**. It pushed ideas in **wafer-scale-style tiling**, dense interconnect, and custom datatypes. However, Tesla reportedly **disbanded the dedicated Dojo team in 2025**, leaning on external AI silicon and its in-car inference chips instead — a reminder that building bespoke supercomputers is hard and costly.

### Trends it influenced
- **Tile/mesh** scaling to reduce chip boundaries
- **Custom datatypes** (configurable FP8) for training
- **Vertical integration** of AI hardware by end users
- Build-vs-buy tradeoffs for bespoke supercomputers

---

## 5. Summary

### Dojo in one paragraph
Dojo was **Tesla's custom AI training supercomputer**, built from its own **D1 chip** and scaled by tiling — **25 D1 dies** form a seamless **Training Tile**, tiles fill cabinets, and many cabinets make an **ExaPOD**. Connected by a high-bandwidth **mesh** and using a configurable **CFP8** datatype, it was tuned specifically for training Tesla's **video-based self-driving** networks. It stands as a bold example of vertical integration, though Tesla reportedly **wound the dedicated program down in 2025**.

### When would something like Dojo make sense?
**A bespoke training machine fits when:**
- You have a **single dominant workload** (here, video training)
- You own **enormous proprietary data**
- You want **full-stack control** of the hardware
- You can absorb the **cost and risk** of custom silicon

**Otherwise**, GPU/TPU clusters or cloud accelerators are usually more practical.

### Future trends
- Tiling/mesh scaling ideas live on (cf. wafer-scale chips)
- Custom training datatypes spreading
- More end-users exploring custom AI silicon — cautiously
- Build-vs-buy remains a central strategic question

> Dojo's lesson: vertical integration can be powerful — but a **bespoke supercomputer is a massive bet**, and even Tesla stepped back from running its own.
