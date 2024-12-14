---
title:  "Enhancing Energy Consumption Predictions for Ships"
mathjax: true
layout: post
categories: 
  = github
  - website
---

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/ai_thesis_logo.png" alt="AI Thesis" style="width: 800px; height: auto;">
</div>

**This work was awarded the Maritime Designer of the Year Award 2022 in the Netherlands, recognizing its significant contribution to the field.**

In my graduate project I developed an innovative approach to accurately predict total dynamic energy consumption for yachts using real operational voyage data. This method aimed to bridge the gap between predicted and actual energy consumption, a significant challenge in the yachting industry driven by the need to reduce environmental impact. Utilizing Grey-Box Modelling (GBM), which combines physics-based White-Box Models (WBM) and data-driven Black-Box Models (BBM), I enhanced both accuracy and extrapolation capacity. By analyzing ten months of continuous monitoring data, hindcasted weather, and voyage information from a Feadship fleet yacht, I achieved predictions for propulsion and auxiliary estimates within 3% and 7% error of operational conditions, respectively.

The process involved developing a sequential modelling methodology that integrated multiple WBMs for different power components and an ANN-based BBM to scale the outputs to fit operational data. Detailed comparisons between WBM, BBM, and GBM categories using external datasets evaluated extrapolation potential, showing GBM improvements over BBM, with limitations related to the strength of dynamic WBM input-output correlations. This project highlighted the significant improvements in accuracy and interpretability offered by combining WBM and BBM. High-quality and relevant input data proved crucial for the success of GBM in predicting energy consumption accurately. Moreover, the modular nature of the GBM allowed for the incorporation of various data types, enhancing its adaptability for different maritime applications.

Ultimately, this project demonstrated the potential of GBM to provide more reliable early-stage energy consumption predictions, helping the yachting industry move towards more sustainable designs. The methodology not only improved prediction accuracy but also offered insights into the dynamic interactions affecting energy consumption, paving the way for future advancements in sustainable yacht design.

# Links to open-access publications

**[Peer-Reviewd Journal Link](https://www.sciencedirect.com/science/article/pii/S2092678222000504?via%3Dihub)**

**[Full MSc. Thesis Link](https://repository.tudelft.nl/record/uuid:949882f3-60c4-484b-8268-40ce38f43830)**
