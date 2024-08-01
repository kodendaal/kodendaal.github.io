---
title:  "An Engineering Approach for Non-Convex Path Optimization"
mathjax: true
layout: post
categories: 
  = github
  - website
---

This project explores various optimization algorithms to minimize travel time for ships in complex maritime environments. This study aimed to address the challenges of efficient voyage planning, which is crucial for cost-effective, energy-efficient, and safe operations. By comparing the **Quasi-Newton BFGS, Particle Swarm, and Simulated Annealing algorithms**, I sought to determine the best optimization tool for scenarios with limited problem information and multiple variables. 

The optimization process included developing a model that interpolates waypoints on a velocity vector field to determine travel time, incorporating linear interpolation for current vectors, and applying a Piece-wise Cubic Hermite Interpolating Polynomial (PCHIP) for smooth path transitions. The model assumed constant ship speed and used a barrier method to handle path obstructions. Through sensitivity analysis and numerical noise investigation, I refined the optimization approach to ensure robustness.

Key learnings from this project include the importance of selecting appropriate optimization algorithms based on the problem's complexity and the benefits of combining different methods to achieve optimal results. The comparison revealed that while each algorithm has its strengths, their performance can vary significantly depending on the specific problem constraints and variables. This project highlighted the practical applications of path optimization in maritime navigation and provided valuable insights into the strengths and limitations of various optimization techniques.

**Note: If the embedded PDF is not displayed properly or if you are viewing this on a mobile device, <a href="https://kodendaal.github.io/assets/project_eng_opti.pdf" target="_blank">please click here</a> to access the PDF directly.**

<div id="adobe-dc-view" style="width: 100%;"></div>
<script src="https://acrobatservices.adobe.com/view-sdk/viewer.js"></script>
<script type="text/javascript">
	document.addEventListener("adobe_dc_view_sdk.ready", function(){ 
		var adobeDCView = new AdobeDC.View({clientId: "8ef44ce133c04e8fa474ad6c78747b08", divId: "adobe-dc-view"});
		adobeDCView.previewFile({
			content:{location: {url: "https://kodendaal.github.io/assets/project_eng_opti.pdf"}},
			metaData:{fileName: "project_eng_opti.pdf"}
		}, {embedMode: "IN_LINE"});
	});
</script>

