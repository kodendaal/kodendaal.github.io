---
title:  "How to Design a Hull: Analyzing Ship Hydrodynamics with BEM"
mathjax: true
layout: post
categories: 
  = github
  - website
---

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/hull_opti.png" alt="Hull Optimization" style="width: 800px; height: auto;">
</div>

What makes a ship cut through the water gracefully while minimizing resistance? It’s all about **hydrodynamics**, and my recent project dove into this fascinating area using modern computational techniques. By implementing a **Boundary Element Method (BEM)**, I explored wave patterns, pressure distributions, and ship motions, all on a custom-designed hull.

---

### The Goal: Simplicity Meets Precision

The objective was to investigate hydrodynamic phenomena using BEM—an efficient computational approach that simplifies complex fluid dynamics. I analyzed:
1. **Wave Patterns**: From bow to stern, understanding the forces acting on the ship.
2. **Pressure Distributions**: Identifying high-pressure zones for hull optimization.
3. **Ship Motions**: Exploring roll, pitch, and heave using Response Amplitude Operators (RAOs).

---

### The Process: Breaking Down the Waves

#### 1. **Custom Hull Design**
Inspired by traditional sailing yachts, I created a custom hull using **Bi-cubic Bezier surfaces**. This technique allowed smooth surface control while meeting specific constraints, such as Froude number limits and a maximum of 500 panels on the wetted surface.

#### 2. **Pre-Processing for BEM**
To prepare the model:
- **Cosine Spacing**: Applied to the wetted surface for finer detail near the bow and stern.
- **Uniform Spacing**: Used on the free surface to capture wave behavior accurately.
- **Grid Optimization**: Ensured the model adhered to theoretical expectations, such as the Kelvin wave angle (~19.5°).

#### 3. **Running the Analysis**
Using the **DELKELV** program, I generated a clear Kelvin wave pattern with two wavelengths along the ship at a Froude number of 0.28. Pressure and velocity analyses offered insights into hull efficiency, highlighting areas with high resistance.

---

### The Results: Riding the Wave of Discovery

1. **Wave Patterns**:
   - Maximum wave heights of **0.06m** were observed at the bow and stern.
   - The stern wave was likely overestimated due to the non-viscous nature of potential flow models.

2. **Pressure Distributions**:
   - High-pressure zones aligned with wave crests.
   - Low-pressure regions indicated areas for potential hull optimization to reduce resistance.

3. **Ship Motions**:
   - **Roll**: Unrealistically high RAO peaks due to the absence of viscous damping.
   - **Heave and Pitch**: Matched expected patterns but revealed areas for improvement in hull stability.

---

### Key Takeaways: Insights into Hydrodynamic Optimization

- **Efficiency vs. Accuracy**: BEM offers quick results but requires thoughtful interpretation due to non-viscous flow assumptions.
- **Grid Design is Critical**: Fine-tuning grid parameters ensures accurate wave and pressure modeling.
- **Understand the Limits**: Knowing the restrictions of potential flow methods, such as the lack of boundary layer effects, is essential for accurate conclusions.

---

### Why It Matters: A Step Forward in Ship Design

This study demonstrates how computational tools like BEM can provide valuable insights into ship hydrodynamics. By combining fast computational times with careful analysis, we can:
- Optimize hull designs for lower resistance and better fuel efficiency.
- Identify areas for structural improvements.
- Accelerate the design process without relying solely on costly experiments.

---

### Sailing Ahead: Bridging Traditional and Modern Techniques

While BEM is a powerful tool, integrating viscous solvers for real-world applications could unlock even greater potential. For now, understanding and leveraging the strengths of potential flow codes gives naval architects a practical edge in designing the ships of tomorrow.

Ready to set sail on a wave of innovation? Let’s navigate the future of naval design together! 🌊⚓️

---

**Note: If the embedded PDF is not displayed properly or if you are viewing this on a mobile device, <a href="https://kodendaal.github.io/assets/numerical_ship_hydro_a1.pdf" target="_blank">please click here</a> to access the PDF directly.**

<div id="adobe-dc-view" style="width: 100%;"></div>
<script src="https://acrobatservices.adobe.com/view-sdk/viewer.js"></script>
<script type="text/javascript">
	document.addEventListener("adobe_dc_view_sdk.ready", function(){ 
		var adobeDCView = new AdobeDC.View({clientId: "79ef659365ef4949aad3901e710fb6e9", divId: "adobe-dc-view"});
		adobeDCView.previewFile({
			content:{location: {url: "https://kodendaal.github.io/assets/numerical_ship_hydro_a1.pdf"}},
			metaData:{fileName: "numerical_ship_hydro_a1.pdf"}
		}, {embedMode: "IN_LINE"});
	});
</script>
