---
title:  "The Art of Choosing the Right Supervised Learning Algorithm"
mathjax: true
layout: post
categories: 
  = github
  - website
---

Supervised learning is a cornerstone of modern machine learning, helping us tackle problems ranging from classifying asteroids to evaluating wine quality. In a recent project, I explored three popular algorithms—**k-Nearest Neighbors (kNN)**, **Support Vector Classifier (SVC)**, and **Multi-Layer Perceptron (MLP)**—to understand their strengths, limitations, and real-world implications. Using the NASA Near-Earth Object and Wine Quality datasets as testing grounds, this study uncovered fascinating insights into the art of algorithm selection. Let’s break it down.

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/supervised_learning.png" alt="Supervised Learning" style="width: 800px; height: auto;">
</div>

---

### The Datasets: Challenges that Make or Break a Model

#### NASA Dataset: Hazardous Asteroids
Imagine trying to predict whether an asteroid could threaten Earth. The NASA dataset, with its **binary classification task**, was built to do just that. However, this data brought unique challenges:
- **Class Imbalance:** 83.89% of asteroids were classified as non-hazardous, making it tricky to identify rare hazardous cases.
- **High Stakes:** Missing a hazardous asteroid is not an option, making recall a critical metric.

#### Wine Quality Dataset: The Complexity of Taste
On the other hand, the Wine Quality dataset had its own set of hurdles:
- **Ordered Multi-Class Labels:** Wine quality scores ranged from poor (3) to excellent (8), requiring models to handle nuanced differences.
- **Class Imbalance:** Some scores appeared more frequently than others, adding to the complexity.

These datasets created the perfect playground for testing how algorithms adapt to real-world problems.

---

### The Approach: Making Comparisons Fair and Square

To ensure a level playing field, I used a standardized methodology:
1. **Data Processing:** Features were standardized to prevent bias from differences in scale.
2. **Cross-Validation:** A 5-fold cross-validation ensured robust performance estimates.
3. **Hyperparameter Tuning:** Grid searches optimized each algorithm, tweaking parameters like the number of neighbors for kNN or the activation function for MLP.
4. **Metrics That Matter:** Beyond accuracy, metrics like precision, recall, and F1-score provided a deeper understanding of model performance.

The result? A fair and insightful comparison across algorithms.

---

### The Results: Winners, Losers, and Trade-Offs

#### NASA Dataset: A Clear Winner
The **MLP algorithm** emerged as the champion, achieving:
- **Accuracy:** 99%
- **F1-Score:** 0.98

Its ability to model complex, non-linear relationships made it ideal for this dataset. However, MLP required longer training times, a trade-off for its impressive performance.

#### Wine Dataset: A Tough Nut to Crack
All three models struggled with the Wine dataset’s complexity. While kNN showed slightly better performance (F1-score: 0.67), the results highlighted the need for more sophisticated techniques to handle **multi-class and imbalanced data**.

---

### Behind the Algorithms: Strengths and Weaknesses

1. **k-Nearest Neighbors (kNN):** 
   - **Strengths:** Simple, quick to train, and effective for local patterns.
   - **Weaknesses:** Sensitive to high-dimensional data and slow during predictions.

2. **Support Vector Classifier (SVC):**
   - **Strengths:** Excellent in high-dimensional spaces, robust with the right regularization.
   - **Weaknesses:** Computationally expensive, particularly for multi-class problems.

3. **Multi-Layer Perceptron (MLP):**
   - **Strengths:** Capable of learning complex patterns, fast predictions thanks to parallelism.
   - **Weaknesses:** Requires significant tuning and training resources.

---

### Lessons Learned and the Road Ahead

This study reinforced a valuable lesson: **there’s no one-size-fits-all algorithm.** The choice depends on the dataset’s structure, complexity, and goals. For imbalanced datasets like NASA, MLP’s non-linear capabilities shine. Meanwhile, simpler models like kNN can perform well on datasets with smoother decision boundaries.

To improve future outcomes, here are some strategies I’d recommend:
- **Address Class Imbalance:** Techniques like oversampling or synthetic data generation (e.g., SMOTE) can level the playing field.
- **Boost Performance with Ensembles:** Combining models through boosting or bagging could mitigate individual weaknesses.
- **Fine-Tune Regularization:** Especially for algorithms like SVC and MLP, optimizing hyperparameters is key to balancing bias and variance.

---

### Final Thoughts: Algorithms in the Real World

Machine learning isn’t just about numbers—it’s about **problem-solving with purpose**. Whether predicting hazardous asteroids or assessing wine quality, the right algorithm can make all the difference. This project underscored the importance of tailoring solutions to the data, balancing trade-offs, and continuously iterating to achieve the best results.

So, the next time you sip a glass of wine or hear about an asteroid narrowly missing Earth, take a moment to appreciate the power of machine learning and the algorithms working behind the scenes.

--- 

**Note: If the embedded PDF is not displayed properly or if you are viewing this on a mobile device, <a href="https://kodendaal.github.io/assets/supervised_learning.pdf" target="_blank">please click here</a> to access the PDF directly.**

<div id="adobe-dc-view" style="width: 100%;"></div>
<script src="https://acrobatservices.adobe.com/view-sdk/viewer.js"></script>
<script type="text/javascript">
	document.addEventListener("adobe_dc_view_sdk.ready", function(){ 
		var adobeDCView = new AdobeDC.View({clientId: "88fc5e85e52f40a8907929f42cf063cb", divId: "adobe-dc-view"});
		adobeDCView.previewFile({
			content:{location: {url: "https://kodendaal.github.io/assets/supervised_learning.pdf"}},
			metaData:{fileName: "supervised_learning.pdf"}
		}, {embedMode: "IN_LINE"});
	});
</script>
