---
title:  "Navigating the High Seas of Optimization: Finding the Fastest Path for Ships"
mathjax: true
layout: post
categories: 
  = github
  - website
---

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/maze_logo.png" alt="route maze" style="width: 800px; height: auto;">
</div>

What’s the fastest way to navigate a ship through complex maritime environments? This question inspired my latest project, where I explored cutting-edge optimization techniques to minimize ship travel time. From battling ocean currents to avoiding islands, this research combines technical precision with real-world challenges. And yes, it’s as exciting as it sounds!

---

### The Challenge: Optimizing Ship Travel

Voyage planning for ships isn’t just about getting from point A to point B—it’s about doing so efficiently, cost-effectively, and safely. The problem gets tricky when you add unpredictable factors like ocean currents and obstructions. That’s where **optimization algorithms** come into play. My project compared three of them:
1. **Quasi-Newton BFGS**: A local optimizer known for its precision.
2. **Particle Swarm Optimization**: A swarm-inspired method excelling in non-linear spaces.
3. **Simulated Annealing**: A physics-inspired algorithm mimicking the cooling of metals.

---

### The Approach: Modeling the Ocean

To simulate real-world conditions, I built a model that:
- **Interpolates Waypoints**: Determines ship paths on a velocity vector field.
- **Handles Obstructions**: Introduces islands as constraints using a barrier method.
- **Ensures Smooth Transitions**: Applies Piece-wise Cubic Hermite Interpolating Polynomial (PCHIP) for realistic path shapes.

The model assumed constant ship speed and simplified variables for computational efficiency. Using sensitivity analysis, I tested the model's robustness, ensuring accuracy amidst numerical noise.

---

### The Results: Picking the Right Algorithm

Here’s how each algorithm performed:
- **Quasi-Newton BFGS**: Precise but struggled with barriers like islands, often settling in local optima.
- **Particle Swarm**: The star performer, consistently finding the fastest path even in complex scenarios.
- **Simulated Annealing**: Both my self-scripted and MATLAB versions were effective, with MATLAB being faster and more robust.

For simple routes, all algorithms worked well, but when islands and multiple variables were added, Particle Swarm and Simulated Annealing outshone Quasi-Newton.

---

### Key Insights: Lessons from the Sea

1. **Adapt the Algorithm to the Problem**:
   - Use **Particle Swarm** for complex, multi-modal problems.
   - Combine with **Quasi-Newton** for refining results in simpler cases.

2. **Realistic Modeling Matters**:
   - Adding obstructions like islands highlighted each algorithm's strengths and weaknesses.
   - Smooth path transitions improved accuracy without sacrificing speed.

3. **Efficiency is Key**:
   - Balancing computational demand with accuracy is crucial. The barrier method, for instance, simplified constraints without overly taxing the system.

---

### Why It Matters: Real-World Applications

This research has practical implications for maritime navigation:
- **Fuel Efficiency**: Optimized paths reduce energy consumption.
- **Cost Savings**: Faster voyages mean lower operational costs.
- **Safety Enhancements**: Avoiding hazards ensures smoother, safer sailing.

---

### Anchors Aweigh: What’s Next?

Future improvements could include incorporating real-world weather data, refining barrier methods, and testing additional algorithms. The goal? To make maritime navigation smarter, faster, and more reliable. Whether it’s for commercial shipping or competitive racing, optimization is the compass pointing us toward innovation.

Let’s set sail into a future of efficient and exciting maritime exploration! 🚢✨

---

**Note: If the embedded PDF is not displayed properly or if you are viewing this on a mobile device, <a href="https://kodendaal.github.io/assets/project_eng_opti.pdf" target="_blank">please click here</a> to access the PDF directly.**

<div id="adobe-dc-view" style="width: 100%;"></div>
<script src="https://acrobatservices.adobe.com/view-sdk/viewer.js"></script>
<script type="text/javascript">
	document.addEventListener("adobe_dc_view_sdk.ready", function(){ 
		var adobeDCView = new AdobeDC.View({clientId: "db69ee87b1ce49cfbefae8d264f647d1", divId: "adobe-dc-view"});
		adobeDCView.previewFile({
			content:{location: {url: "https://kodendaal.github.io/assets/project_eng_opti.pdf"}},
			metaData:{fileName: "project_eng_opti.pdf"}
		}, {embedMode: "IN_LINE"});
	});
</script>

