---
title:  "A step in the Right Direction: Surrogates and Optimization Workshop"
mathjax: true
layout: post
categories: 
  = github
  - website
---

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/surrogate_optimization.png" alt="surrogate optimization" style="width: 800px; height: auto;">
</div>


This interactive blog demonstrates how **data preparation**, **surrogate modeling**, **active learning**, and **optimization** methods can be applied to real engineering design problems.
Interactive demos show:

* **Mooring Line Optimization** — data-science workflow (EDA, surrogate models, validation).
* **Hull Form Optimization** — multi-fidelity workflow combining low- and high-fidelity simulations.
* **Adaptive Learning** — Bayesian optimization that selects new samples based on model uncertainty.


**Note: If the embedded Huggingface Spaces are not loaded properly or if you are viewing this on a mobile device, please click on the usecase links directly.**

---

## Usecase 1: Mooring Line Optimization (Data Science Workflow)

Interactive demo:
[Usecase 1 Link](https://kode24-usecase-1-ds-workflow.hf.space)


<script
	type="module"
	src="https://gradio.s3-us-west-2.amazonaws.com/5.34.2/gradio.js"
></script>

<gradio-app src="https://kode24-usecase-1-ds-workflow.hf.space"></gradio-app>


### Why It Matters

* Mooring layout affects operability and safety.
* Data cleaning and surrogate modeling reduce costly simulation cycles.

---

### Objective

Accelerate optimization of **mooring line parameters** by replacing repeated simulations with surrogate models.

**Design variables**

* `feature_diameter_mm`
* `feature_anchorRadius_m`
* `feature_f_ml_length`

**Performance targets**

* `target_MooringMass_t`
* `target_MaxLoads_N`
* `target_MaxLoads_norm_by_displ`

Goal: **minimize load** while keeping **mass low**.

---

### Workflow Overview

1. **Exploratory Data Analysis**

   * Inspect distributions, correlations, and outliers.

2. **Modeling**

   * Compare Linear, Ridge, RF, and GP models (R², RMSE, residuals).

3. **Cross-Validation**

   * 5–10 fold CV to assess generalization.

4. **Optimization**

   * GA (single objective) or NSGA-II (multi-objective).
   * Visualize Pareto trade-offs.

---

### Key Observations

* Diameter and anchor radius strongly influence mass and load.
* GP models perform well for small datasets.
* CV results show high accuracy (R² > 0.95, RMSE < 5%).
* NSGA-II identifies balanced mass–load trade-offs.

---

### Learning Outcomes

* Surrogates enable rapid design exploration.
* Cross-validation increases confidence in predictions.
* Multi-objective optimization clarifies trade-offs.
* Workflow generalizes to many engineering applications.

---

## Usecase 2: Hull Form Optimization (Multi-Fidelity Workflow)

Interactive demo:
[Usecase 2 Link](https://kode24-usecase-2-mf.hf.space)


<script
	type="module"
	src="https://gradio.s3-us-west-2.amazonaws.com/5.49.1/gradio.js"
></script>

<gradio-app src="https://kode24-usecase-2-mf.hf.space"></gradio-app>


### Why It Matters

* High-fidelity CFD is expensive.
* Multi-fidelity strategies reduce cost by mixing LF and HF samples.

---

### Overview

Minimize calm-water **resistance** using 14 design parameters with bounds ([-1, 1]).

Three fidelity levels differ in mesh density, cost, and accuracy.
Multi-fidelity learning uses many LF samples plus a few HF samples to improve prediction quality within a fixed compute budget.

---

### Simulation Fidelity Summary

| Fidelity | Total Nodes | Resistance [N] | Grid Error [%] | NCC  |
| -------- | ----------- | -------------- | -------------- | ---- |
| High     | 16.5k       | 41.5           | 1.16           | 1.00 |
| Medium   | 5.7k        | 43.5           | 5.97           | 0.11 |
| Low      | 2.1k        | 48.9           | 19.3           | 0.03 |

Diagnostics include Pearson *r*, BPB, and Kendall *τ* to judge MF suitability.

---

### Workflow Overview

1. **Reference & DoE**

   * Generate HF/LF samples that meet the set computational budget.

2. **Modeling**

   * GP surrogate with Matern kernel + WhiteKernel.

3. **Diagnostics & Comparison**

   * Compare MF vs HF-only vs LF-only at equal cost using RMSE and parity plots.

---

### Key Observations

* MF often achieves **better accuracy per computational cost** than HF-only.
* Too little HF weakens LF→HF correlation; too much HF reduces MF benefit.
* Diagnostics help determine when MF is appropriate.

---

### Learning Outcomes

* MF modeling balances accuracy and cost.
* Proper diagnostics guide sampling allocation.
* Valid comparisons require equal computational budgets.

---

## Usecase 3: Active Learning (Bayesian Optimization Workflow)

Interactive demo:

[Usecase 3 Link](https://kode24-usecase-3-active-learn.hf.space)

<script
	type="module"
	src="https://gradio.s3-us-west-2.amazonaws.com/5.49.1/gradio.js"
></script>

<gradio-app src="https://kode24-usecase-3-active-learn.hf.space"></gradio-app>

### Why It Matters

* Expensive simulations limit dataset size.
* Adaptive sampling focuses effort where uncertainty or expected improvement is highest.

---

### Objective

Introduce adaptive learning / Bayesian optimization:

* **Single-objective**: GP + Expected Improvement (EI).
* **Multi-objective**: GP + Expected Hypervolume Improvement (EHVI).
* ** Propeller Optimization: Real-world case for multi-objective EHVI application

---

### Workflow Overview

1. **Initialize**

   * Small DoE (5–10 samples).
   * GP with Matern kernel.

2. **Acquire**

   * Evaluate EI or HVI to select next samples.

3. **Evaluate**

   * Run simulation or function at selected point.

4. **Update**

   * Retrain and repeat until convergence or budget limit.

---

### Key Observations

* EI efficiently finds global minima with few evaluations.
* HVI steadily expands the Pareto front and tracks progress via hypervolume.
* Same approach applies to expensive engineering simulations.

---

### Learning Outcomes

* Bayesian optimization intelligently balances exploration vs. exploitation.
* Matern kernels suit smooth engineering responses.
* EI works well for small datasets; HVI extends BO to multi-objective problems.
* Adaptive workflows support efficient experimental or simulation-based design.

---










