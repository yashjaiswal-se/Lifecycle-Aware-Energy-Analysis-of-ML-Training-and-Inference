# Lifecycle-Aware Energy Optimization for Machine Learning Systems

## Overview
This repository contains an empirical research project that investigates **lifecycle-level energy trade-offs in machine learning systems**, with a focus on the **joint contribution of training and inference energy**.

Rather than optimizing models solely for accuracy or isolated efficiency metrics, this project evaluates **total lifecycle energy cost** under realistic deployment assumptions, where training energy is amortized over a varying number of inference runs.

The core objective is to demonstrate that **accuracy-optimal models are not necessarily lifecycle-optimal**, and that optimal design choices depend strongly on deployment scale.

---

## Key Contributions
- **Lifecycle formulation** of ML energy consumption combining training and inference:
  
  \[
  E_{\text{total}} = E_{\text{train}} + N \cdot E_{\text{inference}}
  \]

- **Joint training–inference analysis** showing deployment-scale-dependent optimality
- Introduction of **Energy per Correct Prediction (ECP)** as a practical lifecycle metric
- Empirical evaluation of how model ranking changes with deployment size
- Reproducible energy measurement methodology for ML experiments

---

## Experimental Scope and Limitations
This project is intentionally scoped to:
- CNN-based supervised learning workloads
- Image classification benchmarks
- GPU-based training and inference
- Energy measured at the device level (power × time)

The framework is **not claimed to generalize** to all ML paradigms, hardware platforms, or application domains. The goal is **empirical evidence and evaluation methodology**, not universal optimization guarantees.

---

## Repository Structure
```

.
├── phase1/                 # Reproducible energy measurement baseline
├── phase2/                 # Training-side energy–accuracy optimization
├── phase3/                 # Inference-side energy optimization
├── phase4/                 # Lifecycle integration and deployment-scale analysis
└── README.md

```

---

## Methodology Summary
1. **Baseline Measurement**  
   Establish reproducible energy logging for training and inference runs.

2. **Training Optimization**  
   Analyze energy–accuracy trade-offs using early stopping and energy-regularized objectives.

3. **Inference Optimization**  
   Measure inference energy under multiple precision and execution settings.

4. **Lifecycle Integration**  
   Combine training and inference energy across deployment scales and evaluate model rankings using ECP.

---

## Metrics
- Accuracy
- Training energy consumption
- Inference energy per sample
- Total lifecycle energy
- **Energy per Correct Prediction (ECP)**

---

## Reproducibility
All experiments are conducted with:
- Fixed random seeds
- Explicit hardware documentation
- Logged power and execution time
- Scripted evaluation pipelines

Exact environment details and configurations are documented within each phase directory.

---

## Intended Use
This repository is intended for:
- Academic research and reproducibility
- Capstone or thesis-level projects
- Systems-oriented ML energy evaluation
- Methodological reference for lifecycle-aware analysis

It is **not** intended as a production optimization library.

---

## Citation
If you use or build upon this work, please cite appropriately.  
A formal publication reference will be added upon acceptance.

---

## License
This project is released under an open-source license for research and educational use.
```

