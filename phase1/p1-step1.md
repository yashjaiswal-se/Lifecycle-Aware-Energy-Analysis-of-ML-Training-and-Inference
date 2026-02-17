# Phase 1 — Step 1: Measurement Specification Lock

## Goal
Produce a **frozen, reviewer-proof definition of “energy”** that remains unchanged for the remainder of the paper.  
This step establishes a precise measurement claim and prevents ambiguity or post-hoc reinterpretation.

---

## 1.1 Core Question
**What physical quantity is being measured?**

We measure the **total GPU energy consumed during model training**, computed by integrating the GPU’s instantaneous power draw over the full wall-clock duration of training.

---

## 1.2 Mathematical Definition

\[
E_{\text{train}} = \int_{t_{\text{start}}}^{t_{\text{end}}} P_{\text{GPU}}(t)\, dt
\]

### Term Definitions
- **\(P_{\text{GPU}}(t)\)**: Instantaneous GPU power draw reported by the device (Watts)  
- **\(t_{\text{start}}\)**: Moment immediately before the first training operation begins  
- **\(t_{\text{end}}\)**: Moment immediately after the final training operation completes  
- **Unit of \(E_{\text{train}}\)**: Joules (J)

---

## 1.3 Temporal Scope

### Included Time
The measurement includes **all GPU activity during wall-clock training**, specifically:
- Forward propagation  
- Backward propagation  
- Optimizer updates  
- Kernel launches  
- Synchronization overhead  
- GPU idle time caused by data loading or framework stalls  
- Model checkpointing performed during training (e.g., periodic state saves)

### Excluded Time
The following are explicitly excluded:
- Dataset download or preparation  
- Post-training evaluation (unless explicitly stated otherwise)  
- Experiment setup prior to training start  

📌 **Reviewer Concern Addressed**  
> *“Did you measure kernel execution only, or actual training energy?”*

**Answer:** Actual **wall-clock training energy**.

Checkpointing is treated as part of the standard training procedure in practical workflows. Excluding it would underestimate the true energy incurred during training.

---

## 1.4 Hardware Scope

### Device Scope
- **Included:** Single GPU energy consumption  
- **Excluded:** CPU, system DRAM, storage, networking, and cooling infrastructure  

**Rationale:**  
We focus on GPU energy because it dominates training energy consumption in modern ML workloads and can be measured reproducibly across runs and systems. This choice is consistent with established practice in Green AI measurement studies.

---

## 1.5 Measurement Signal

- **Observed signal:** Instantaneous GPU power draw (Watts)  
- **Source:** Vendor-reported GPU power telemetry  
- **Measurement type:** Sampled at fixed time intervals  

### Explicitly Not Used
- Energy counters  
- FLOPs × TDP–based estimates  
- Carbon or emissions proxies  

---

## 1.6 Exclusion Rationale

| Excluded Component | Reason |
|------------------|--------|
| CPU | Secondary contribution; difficult to isolate reproducibly |
| DRAM | Platform-dependent; not consistently accessible |
| Cooling / PUE | Datacenter-specific; outside model design space |
| Carbon | Policy-layer metric, not direct energy measurement |

These exclusions follow established practice in early Green AI measurement work and enable controlled, reproducible comparisons.

---

## 1.7 Granularity and Numerical Integration
- GPU power is sampled **discretely over time**  
- Energy is computed via **numerical integration** of sampled power values  
- Integration is performed over **observed measurements**, not inferred execution traces  

---

## 1.8 Explicit Non-Claims

This measurement does **not** claim to be:
- A full system energy measurement  
- A datacenter-level energy estimate  
- A carbon footprint  
- An efficiency metric by itself  

These non-claims prevent over-interpretation of the reported results.

---


