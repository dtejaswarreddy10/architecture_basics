# LPU — Language Processing Unit (Groq)

> **Essence:** A chip built for *blazing-fast, predictable* AI inference. Groq removes all the guesswork inside the processor — the **compiler schedules every operation in advance**, so there are no surprises and no waiting.

---

## 1. Introduction

### What is an LPU?
An **LPU (Language Processing Unit)** is an AI inference chip from **Groq**, designed to run large language models with **extremely low and predictable latency** — generating tokens at record speed. Its underlying architecture is the **TSP (Tensor Streaming Processor)**.

- A **GPU** decides *at runtime* what each core does (dynamic, complex).
- An **LPU** decides *at compile time* — **everything is pre-planned**.

### Where did LPUs come from?
Groq (founded 2016 by **Jonathan Ross**, who helped create Google's TPU) targeted the biggest pain in serving LLMs: **inconsistent, unpredictable latency**. GPUs are fast on average but jittery, because caches, schedulers, and branch predictors make timing variable. Groq's answer: **remove all that nondeterminism**.

### The main idea behind LPU design
> **Make the hardware perfectly predictable by letting software schedule everything.**

No caches, no branch prediction, no dynamic scheduling. The **compiler** maps out exactly which operation runs on which unit at which **cycle** — "software-defined hardware." The result is **deterministic, ultra-low latency**.

---

## 2. Basic Functionality & Architecture

### Simple analogy: a perfectly choreographed dance
A GPU is a busy kitchen where chefs improvise and sometimes bump into each other. The LPU is a **perfectly choreographed dance** — every move is planned in advance, so it runs at full speed with **no collisions and no waiting**.

### Tensor Streaming Processor (TSP)
- Data **streams** through functional units in a planned, assembly-line fashion.
- Compute units (matrix, vector, memory) are arranged so results **flow** from one to the next.
- The **compiler** schedules every operation cycle-by-cycle — the hardware just executes the plan.

### What Groq removed (on purpose)
| Typical CPU/GPU feature | LPU |
|--------------------------|-----|
| Caches | ❌ removed — uses fast on-chip SRAM directly |
| Branch prediction | ❌ removed |
| Out-of-order / dynamic scheduling | ❌ removed |
| Result | ✅ **Fully deterministic timing** |

### Deterministic = fast *and* scalable
Because timing is exact, Groq can chain **many chips together** and still predict behavior perfectly — so multi-chip systems stay efficient with no synchronization guesswork. This is a big reason the LPU posts such high **tokens-per-second** on LLMs.

### LPU vs GPU (for inference)

| Feature | GPU | LPU |
|---------|-----|-----|
| Scheduling | Dynamic (runtime) | **Static (compiler)** |
| Latency | Fast but variable | **Low &amp; deterministic** |
| Caches | Yes | **None — direct SRAM** |
| Best at | Training + inference | **Fast LLM inference** |
| Token speed | High | **Often record-setting** |

---

## 3. Applications

### Where LPUs shine
- 💬 **Real-time LLM inference** — chatbots, assistants, agents
- ⚡ **Low-latency token generation** — fast, responsive replies
- 🔌 **AI APIs / inference-as-a-service** (GroqCloud)
- 🏢 **Latency-critical enterprise AI**
- 🧠 Any service where **response time** is the product

### Why pick an LPU?
- **Lowest, most predictable latency** for LLMs
- **Record token-generation speed**
- **Deterministic** → easy to guarantee service levels
- Efficient **multi-chip** scaling

### What LPUs are NOT for
- Large-scale **training** → **GPU/TPU/WSE**
- General-purpose computing → **CPU**
- Graphics → **GPU**
- Workloads that aren't inference-shaped

---

## 4. Market Examples & Future

### Products & ecosystem
| Item | Note |
|------|------|
| **GroqChip (TSP)** | The LPU silicon — deterministic streaming processor |
| **GroqCard / GroqNode** | Cards and systems for the data center |
| **GroqCloud** | Cloud API delivering very fast LLM inference |
| **Groq Compiler** | Does the heavy lifting — schedules everything |

### Business context
Groq made headlines with **demos generating hundreds of tokens per second**, far faster than typical GPU inference. It positions the LPU as the chip for the **inference era** of AI, where serving models quickly and cheaply matters more than training them.

### Trends
- AI shifting from **training-heavy** to **inference-heavy** — Groq's sweet spot
- Pushing **tokens-per-second** ever higher
- **Deterministic** multi-chip systems
- Inference-as-a-service via the cloud

---

## 5. Summary

### LPU in one paragraph
The LPU is Groq's AI inference processor, built on a **Tensor Streaming Processor** that removes caches, branch prediction, and dynamic scheduling so the **compiler can plan every operation cycle-by-cycle**. This makes timing fully **deterministic**, delivering the **lowest, most predictable latency** and record token-generation speeds for large language models — at the cost of being specialized for inference, not training.

### When should you choose an LPU?
**An LPU is the right tool when:**
- You serve **LLMs** and need **fast, predictable** responses
- **Latency** is critical to the product
- You want **guaranteed** (deterministic) performance
- You're in the **inference** phase, not training

**Use a GPU/TPU/WSE** for training and flexible compute.

### Future trends
- The "inference era" plays to the LPU's strengths
- Ever-higher tokens-per-second
- Deterministic large-scale systems
- Fast, cheap inference as a cloud service

> The LPU's bet: in a world of AI assistants, **speed and predictability** of inference win.
