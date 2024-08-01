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

<iframe src="https://kodendaal.github.io/assets/project_eng_opti.pdf" type="application/pdf" style="overflow: false; -webkit-overflow-scrolling: touch; border: none;" scrolling="yes" width="100%" height="1050"> </iframe>


