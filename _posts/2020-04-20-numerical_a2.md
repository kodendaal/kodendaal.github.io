---
title:  "Riding the Waves: Investigating Planing Vessel Hydrodynamics with Modern Tools"
mathjax: true
layout: post
categories: 
  = github
  - website
---

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/wedges_logo1.png" alt="Wedges CFD" style="width: 800px; height: auto;">
</div>

Ever wonder what keeps a high-speed planing vessel gliding smoothly across the water? The answer lies in **hydrodynamics**, a fascinating field that blends physics, fluid mechanics, and engineering. My latest project explored this by comparing traditional and modern methods to analyze the behavior of planing vessels.

---

### The Challenge: Traditional vs. Modern Techniques

Historically, towing tank experiments were the go-to for understanding planing vessel hydrodynamics. However, with advancements in **Computational Fluid Dynamics (CFD)**, we now have tools that promise detailed and flexible insights. This project aimed to compare:
1. **Savitsky’s Method**: A classic analytical approach for planing hulls.
2. **Von Karman’s Method**: A momentum-based analytical technique.
3. **CFD Simulations**: The modern, computational powerhouse.

---

### The Approach: From Geometry to Simulation

#### Step 1: Define the Geometry
Using **Savitsky’s Method**, I calculated key parameters like trim angle, draft, and wetted keel length. These parameters provided a solid foundation for modeling and ensured consistency across methods.

#### Step 2: Mesh Generation for CFD
Creating a reliable CFD mesh is an art and a science:
- **Balancing Accuracy and Efficiency**: Six mesh sizes were tested, ranging from 3,649 to over 100,000 elements.
- **Refining Key Areas**: Extra focus on the wedge region ensured precise force calculations.

#### Step 3: Running the CFD Simulations
CFD involves numerous parameters, including solver type, time-stepping, and diffusion settings. Through **trial and error**, I fine-tuned these parameters to achieve stable and realistic results. The simulations revealed:
- Pressure distributions across the hull.
- Velocity fields highlighting fluid behavior.
- Detailed force calculations over time.

---

### The Results: Comparing Methods

1. **CFD**:
   - Provided the most detailed insights, capturing dynamic fluid interactions like vortex formation and pressure redistribution.
   - Required significant computational resources but delivered highly accurate results.

2. **Savitsky’s Method**:
   - Quick and computationally light.
   - Useful for approximations but lacked the depth of CFD.

3. **Von Karman’s Method**:
   - Overestimated forces due to simplified assumptions.
   - Adjustments for fluid acceleration improved results but still lagged behind CFD.

---

### Key Takeaways: Lessons from the Water

- **Accuracy vs. Efficiency**: While analytical methods like Savitsky’s are great for initial approximations, CFD is unparalleled for detailed analysis.
- **Parameter Selection Matters**: Fine-tuning CFD inputs is critical for realistic simulations.
- **Mesh Refinement is Crucial**: The accuracy of CFD results depends heavily on mesh quality, especially near high-impact areas.

---

### Why It Matters: The Future of Ship Design

This project highlights the growing importance of CFD in modern ship design. By offering detailed insights into fluid dynamics, CFD enables:
- **Better Performance**: Optimizing hull designs for speed and efficiency.
- **Cost Savings**: Reducing the need for physical experiments.
- **Flexibility**: Adapting to complex, real-world scenarios.

---

### Charting New Waters

Looking ahead, the combination of traditional methods and CFD holds immense potential. Analytical techniques provide a quick starting point, while CFD adds depth and precision. Together, they pave the way for innovative, efficient, and sustainable ship designs.

Ready to ride the waves of hydrodynamic innovation? Let’s make a splash! 🌊✨

---

**Note: If the embedded PDF is not displayed properly or if you are viewing this on a mobile device, <a href="https://kodendaal.github.io/assets/numerical_ship_hydro_a2.pdf" target="_blank">please click here</a> to access the PDF directly.**

<div id="adobe-dc-view" style="width: 100%;"></div>
<script src="https://acrobatservices.adobe.com/view-sdk/viewer.js"></script>
<script type="text/javascript">
	document.addEventListener("adobe_dc_view_sdk.ready", function(){ 
		var adobeDCView = new AdobeDC.View({clientId: "db69ee87b1ce49cfbefae8d264f647d1", divId: "adobe-dc-view"});
		adobeDCView.previewFile({
			content:{location: {url: "https://kodendaal.github.io/assets/numerical_ship_hydro_a2.pdf"}},
			metaData:{fileName: "numerical_ship_hydro_a2.pdf"}
		}, {embedMode: "IN_LINE"});
	});
</script>

