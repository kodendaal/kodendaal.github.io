---
title:  "Numerical Assessment and Approximation of Planing Hull Ships"
mathjax: true
layout: post
categories: 
  = github
  - website
---

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/wedges_logo.png" alt="Wedges CFD" style="width: 800px; height: auto;">
</div>


In this project, I investigated the hydrodynamic characteristics of planing vessels using various computational methods. Traditionally, these characteristics were studied through towing tank experiments, but with advancements in technology, Computational Fluid Dynamics (CFD) has become increasingly relevant. This study compared the results of hydrodynamic calculations using CFD, Savitsky’s Method, and Von Karman’s Method to validate and understand the differences between these approaches.

The project began by determining the key parameters of the vessel geometry using Savitsky’s hydrodynamic design, which provided a close approximation of planing craft. These parameters included trim angle, draft, wetted keel length, and inclined dead rise angle, which were crucial for the study. A significant part of the project involved generating a mesh for CFD analysis, balancing computational efficiency and accuracy. Different mesh sizes were tested to ensure the results were robust and reliable.

The CFD analysis required careful selection of parameters, such as solver type, artificial diffusion, and time-stepping methods. Through extensive trial and error, I refined these parameters to achieve stable and accurate simulations. The visualization of results highlighted the fluid dynamics around the planing hull, including pressure distributions and velocity fields, providing insights into the performance and behavior of the vessel under different conditions.

Key learnings from this project include the importance of choosing the right computational methods and parameters for accurate hydrodynamic analysis. The comparison of CFD with traditional analytical methods demonstrated the advantages and limitations of each approach. This study underscores the potential of CFD in modern ship design, offering a more flexible and detailed analysis compared to traditional methods.

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

