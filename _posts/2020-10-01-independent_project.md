---
title:  "Enhancing Ship Hull Design Efficiency Through Sensitivity Analysis"
mathjax: true
layout: post
categories: 
  = github
  - website
---

In this independent research project, I explored a critical aspect of ship design: the longitudinal strength of hulls, which is essential for preventing catastrophic failures like fracturing or sinking. The challenge I faced was the complex and time-consuming process of calculating this strength, which involves meticulously inputting up to 5000 individual weight items to model the vessel’s weight distribution. My goal was to streamline this process by applying a detailed sensitivity analysis to evaluate different weight distribution techniques and their impact on longitudinal strength parameters.

I focused on three weight distribution techniques: approximate parabolic, point-wise grouping, and trapezoidal direct. Through a local one-at-a-time sensitivity analysis, I assessed how each method affects still water shear force and bending moment, adhering to a general accuracy requirement of ±10%. My initial findings showed that the parabolic approximation method did not meet the accuracy requirements. Consequently, I expanded the analysis to a large-scale case study with Damen Yachting, using real data to compare the techniques.

The results revealed that both the grouping and trapezoidal methods performed well in handling longitudinal strength calculations. The trapezoidal method offered slightly better accuracy (0.22% and 0.35% improvements in shear and bending moment, respectively). Although the grouping method had lower accuracy (0.38% and 3.49% deviations), it was advantageous for academic purposes due to its superior weight input control. Notably, when distributed loads were simplified to individual point loads, the results deviated significantly from the baseline metrics.

Using the local sensitivity methodology, I found that not grouping items resulted in a significant reduction in input time by 29.88% compared to full input scenarios. Additionally, two vessel verification studies confirmed further time reductions of 24.97% and 27.00%, with the accuracy of the elbow point metric varying only between 0.3% and 2.3% from fully detailed cases. Overall, my work demonstrated time savings of 30% to 25%, showcasing a substantial improvement in efficiency for ship hull design.

This research highlights the potential for significant time and resource savings in ship design through effective weight distribution techniques and sensitivity analysis. By optimizing the weight input process, I was able to streamline the engineering process and enhance the accuracy of longitudinal strength calculations.

<embed src="https://kodendaal.github.io/assets/project_independent.pdf" type="application/pdf" width="750" height="1050" />
