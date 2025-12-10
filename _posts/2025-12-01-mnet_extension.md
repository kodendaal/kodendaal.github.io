---
title:  "When 2D Meets 3D: Rethinking Medical Segmentation Through MNet"
mathjax: true
layout: post
categories: 
  = github
  - website
---

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/mnet.png" alt="mnet" style="width: 800px; height: auto;">
</div>


*A concise technical walkthrough of our MNet replication and architectural improvements*

---

Modern medical imaging—MRI and CT in particular—often suffers from *anisotropy*: slices may be spaced far apart along the z-axis while in-plane resolution remains high. This mismatch creates a persistent challenge for 3D segmentation models. Pure 3D CNNs tend to overfit sparse depth information; pure 2D CNNs ignore valuable volumetric context.

**MNet** was proposed as a hybrid 2D/3D architecture that blends both perspectives at every stage of the network. In this project, we **reproduced MNet from scratch**, validated its core claims, and designed two lightweight extensions—**Fusion Gating** and **VMamba**—to push the architecture further.

Below is a brief look at *what we reproduced*, *how we improved it*, and *what we learned*.

---

# 🔍 Why MNet?

MNet introduces a *mesh-like* U-Net architecture with parallel 2D and 3D encoder-decoder branches. Instead of choosing between 2D or 3D convolutions, MNet blends both inside each block using manually defined fusion rules (add / subtract / concatenate).

According to the authors, this yields strong robustness to anisotropy across MRI and CT datasets.

Our goals were:

1. **Reproduce MNet** and verify the original performance trends.
2. **Test its robustness** under controlled z-spacing perturbations.
3. **Extend MNet** by introducing:

   * **Fusion Gating** → learnable 2D–3D blending
   * **VMamba** → efficient long-range depth modeling via state-space modules

---

# 📦 Experimental Setup

We used nnU-Net v1 pipelines for preprocessing, augmentation, and patch sampling—matching the original implementation as closely as possible.
Datasets:

* **PROMISE12 (MRI prostate)** – strongly anisotropic MRI
* **LiTS (CT liver & tumors)** – much more isotropic, but tumor segmentation is notoriously difficult

Training was performed on 16-GB GPUs (Lightning.ai), so long schedules (500 epochs) were not feasible. Instead, we trained for **150 epochs**, and validated that PROMISE converges by epoch ~100–120.

---

# ✅ Reproducing MNet

Our reproduction closely matched the original paper’s reported numbers:

### PROMISE12

* **Original MNet:** 89.8% Dice
* **Our reproduction:** **89.0 ± 0.9%**

### LiTS

* **Liver:** 94.3 ± 1.9% (matches original 94.3%)
* **Tumor:** 54.6 ± 3.1% (expected drop due to 50-case subset)

> **Conclusion:** We successfully reproduced MNet within acceptable reproducibility margins (±2–3 Dice), confirming the architecture’s validity.
>

---

# 🧩 Extension 1: Fusion Gating

The original MNet uses *fixed* operations to merge 2D and 3D feature streams. But fixed rules cannot adapt to variations in local anatomy, noise, or slice spacing.

We replaced them with **learnable gates** that estimate “trust” between 2D and 3D features either:

* **Channel-wise:** one gate per feature channel
* **Spatial-wise:** one gate per voxel location

Gating performs soft interpolation:

[
y = g \odot x_{2D} + (1-g) \odot x_{3D}
]

Result:

* **Spatial Gating improved PROMISE Dice from 89.0 → 90.0%**
* Added *negligible compute overhead*
* Provided smoother boundary predictions


---

# 🧩 Extension 2: VMamba for Depth Modeling

3D convolutions struggle with long-range dependencies when z-resolution is coarse. Attention-based models help, but are expensive in 3D.

We integrated **VMamba**, a state-space model performing efficient z-axis scanning:

* Models each (H, W) pixel as a sequence along depth
* Achieves **O(D)** complexity instead of the quadratic cost of attention
* Replaces heavy 3D convolutions in deeper bottleneck layers
* Reduces parameter count from **8.77M → 7.42M**

Results:

* Strongest LiTS *liver* Dice: **95.8 ± 0.7%**
* Improved consistency under anisotropy
* Higher variance for tumor class (due to dataset complexity)


---

# 🎯 Results Summary

### ✔ Reproduction Success

* PROMISE reproduction is within **0.8%** of the original.
* LiTS liver segmentation matches the original exactly.

### ✔ Extensions Help

* **Spatial Gating** → Most stable and consistent improvements
* **VMamba** → Best liver performance; fewer parameters

### ✔ Robust to Anisotropy

Across PROMISE (1–4 mm spacing), Dice only dropped **~1.5 points** for extended variants, outperforming the baseline’s ~2–3 point drop.


---

# 💡 Key Takeaways

* **MNet is indeed reproducible**—its hybrid 2D/3D design is robust and stable.
* **Learned fusion works better than rigid fusion.** Spatial Gating provides a free performance boost with minimal overhead.
* **State-space models (VMamba) are promising for 3D medical imaging**, especially where z-resolution is limited.
* **LiTS tumor segmentation remains a data-limited problem**, not an architectural one.

---

# 🚧 Limitations & Future Directions

Due to compute limitations, LiTS results were based on a 50-case subset and 150-epoch schedules. With full dataset access and extended training, we expect larger gains—especially for VMamba.

Promising next steps:

* Full-resolution LiTS with 500-epoch training
* Stratified cross-validation to mitigate tumor sparsity issues
* Bidirectional VMamba scanning
* Combining learned fusion with modern 3D attention mechanisms

---

# 📘 Closing Thoughts

This project shows that **MNet remains a strong and elegant baseline** for anisotropic medical segmentation—but also that small, thoughtful architectural tweaks can further improve robustness and generalization.

By adding adaptive fusion and efficient global depth modeling, we demonstrate meaningful gains without sacrificing MNet’s lightweight nature.

---

**Note: If the embedded PDF is not displayed properly or if you are viewing this on a mobile device, <a href="https://kodendaal.github.io/assets/CS6250_mnet_final_project_1.pdf" target="_blank">please click here</a> to access the PDF directly.**

<div id="adobe-dc-view" style="width: 100%;"></div>
<script src="https://acrobatservices.adobe.com/view-sdk/viewer.js"></script>
<script type="text/javascript">
	document.addEventListener("adobe_dc_view_sdk.ready", function(){ 
		var adobeDCView = new AdobeDC.View({clientId: "573c32d5dd174f50832b5a2a28c74648", divId: "adobe-dc-view"});
		adobeDCView.previewFile({
			content:{location: {url: "https://kodendaal.github.io/assets/CS6250_mnet_final_project_1.pdf"}},
			metaData:{fileName: "CS6250_mnet_final_project"}
		}, {embedMode: "IN_LINE"});
	});
</script>
