---
title:  "A Hydrodynamic Numerical Assessment of Vessel Performance"
mathjax: true
layout: post
categories: 
  = github
  - website
---


Numerical methods for analyzing ship hydrodynamics have become increasingly important in modern naval architecture. This study implements a Boundary Element Method (BEM) to examine hydrodynamic phenomena on a custom hull geometry. The analysis focuses on wave patterns, pressures, and velocity vectors, as well as ship motions through diffraction techniques.

The investigation begins with an overview of potential flow theory and boundary conditions essential for BEM analysis. A custom hull geometry inspired by traditional sailing yachts was created using Bi-cubic Bezier surfaces. The model was carefully designed to meet specific constraints required by the DELKELV program, including limitations on the Froude number, hull shape, and panel count.

Pre-processing steps involved determining appropriate grid sizes, panel numbers, and spacing techniques. The study used cosine spacing on the wetted surface and uniform spacing on the free surface to capture relevant physics accurately. The analysis produced a clear Kelvin wave pattern with two wavelengths along the vessel, matching theoretical predictions for the given Froude number of 0.28.

Results showed maximum wave heights of about 0.06m at the bow and stern, with the stern wave possibly overestimated due to the potential flow model's limitations. Pressure distribution analysis revealed high-pressure regions corresponding to wave crests and low-pressure areas aligned with troughs. These pressure gradients indicated potential areas for hull geometry optimization to improve flow uniformity and reduce resistance. The study also examined ship motions using Response Amplitude Operators (RAOs) for six degrees of freedom. Particular attention was given to roll, pitch, and heave motions. The analysis highlighted some limitations of potential flow methods, such as the lack of viscous damping in roll motions leading to unrealistically high peaks in the RAO.

While BEM techniques offer fast computational times compared to viscous solvers, the researchers emphasize the importance of understanding non-viscous flow effects to interpret results accurately. The study concludes that potential flow codes can be powerful tools in ship design when used judiciously, with careful consideration of their limitations and thoughtful interpretation of results.

**Note: If the embedded PDF is not displayed properly or if you are viewing this on a mobile device, <a href="https://kodendaal.github.io/assets/numerical_ship_hydro_a1.pdf" target="_blank">please click here</a> to access the PDF directly.**

<iframe src="https://kodendaal.github.io/assets/numerical_ship_hydro_a1.pdf" type="application/pdf" style="overflow: false; -webkit-overflow-scrolling: touch; border: none;" scrolling="yes" width="100%" height="1050"> </iframe>

