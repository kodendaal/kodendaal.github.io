---
title:  "Random Optimization for Machine Learning Applications"
mathjax: true
layout: post
categories: 
  = github
  - website
---

In this exploration, I delved into the world of randomized optimization techniques, **focusing on Random Hill Climbing (RHC), Simulated Annealing (SA), and Genetic Algorithms (GA).** This study aimed to assess the performance and efficiency of these methods on two classic problems—the Four Peaks problem and the Max K-Colour problem—and their application in training neural networks using the Wine Quality dataset. The performance of these optimizers varied significantly depending on the problem, consistent with the no-free-lunch theorem, which posits no single optimizer excels universally.

RHC emerged as the fastest optimizer regarding wall-clock time and required minimal parameter tuning. However, it tended to get stuck in local minima, making it less suitable for complex or highly structured problems, though it performed better on simpler or moderately sized problems. SA, on the other hand, demonstrated the ability to escape local optima by initially accepting worse solutions, performing well on problems with many local minima. Its tunable temperature and cooling schedule provided flexibility, but it was computationally expensive and sensitive to the cooling schedule, requiring careful tuning and exhibiting slower overall convergence compared to RHC and backpropagation (BP) used in neural networks.

GA showed robustness for large, complex problems with many local optima, with its population diversity effectively exploring the solution space. However, it had the longest training time and required significant parameter tuning for population size and mutation rate. Notably, GA showed the lowest performance metrics for the Wine Quality dataset, making it less efficient and cost-effective in this context.

When optimizing neural networks, backpropagation (BP) outperformed the randomized techniques, demonstrating the highest precision and F1-score due to its direct gradient-based approach. SA and RHC had comparable accuracy and recall but lower precision and F1-scores compared to BP, while GA exhibited the poorest performance. This analysis underscores the necessity of tuning individual optimizers and comparing multiple options to identify the best performer for each specific problem. Randomized optimization algorithms are particularly effective in navigating non-differentiable, discontinuous, or irregular optimization landscapes. By carefully selecting and tuning these optimizers, one can achieve tailored solutions that best fit the unique characteristics of each problem.


**Note: If the embedded PDF is not displayed properly or if you are viewing this on a mobile device, <a href="https://kodendaal.github.io/assets/random_optimization.pdf" target="_blank">please click here</a> to access the PDF directly.**

<div id="adobe-dc-view" style="width: 100%;"></div>
<script src="https://acrobatservices.adobe.com/view-sdk/viewer.js"></script>
<script type="text/javascript">
	document.addEventListener("adobe_dc_view_sdk.ready", function(){ 
		var adobeDCView = new AdobeDC.View({clientId: "8ef44ce133c04e8fa474ad6c78747b08", divId: "adobe-dc-view"});
		adobeDCView.previewFile({
			content:{location: {url: "https://kodendaal.github.io/assets/random_optimization.pdf"}},
			metaData:{fileName: "random_optimization.pdf"}
		}, {embedMode: "IN_LINE"});
	});
</script>
