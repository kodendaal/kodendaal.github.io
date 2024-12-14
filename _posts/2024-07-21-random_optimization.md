---
title:  "Quirky World of Randomized Optimization: A Battle of Algorithms"
mathjax: true
layout: post
categories: 
  = github
  - website
---

When you think about optimization, you might imagine a super-smart algorithm breezing through problems with mathematical precision. But what happens when the problem isn’t smooth or straightforward? Enter the quirky stars of this blog post: **Random Hill Climbing (RHC)**, **Simulated Annealing (SA)**, and **Genetic Algorithms (GA)**—a trio of randomized optimization techniques that prove there's more than one way to find a solution.

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/randomness_logo.png" alt="Random Optimization" style="width: 800px; height: auto;">
</div>


In this post, I’ll walk you through my recent exploration into how these algorithms handle tricky optimization puzzles and even step into the shoes of backpropagation (BP) for training neural networks. Spoiler alert: their performance is as diverse as their personalities!

---

## **Meet the Contestants**

**Random Hill Climbing (RHC)**  
RHC is the sprinter of the group—fast, agile, and straightforward. It starts with a random solution, makes small adjustments, and keeps whatever improves the score. But here’s the catch: RHC often gets stuck in local minima, like a hiker who can’t see past the nearest hill. It’s best for simple or moderately sized problems, where its speed really shines.

**Simulated Annealing (SA)**  
SA is the adventurous one. Inspired by the cooling process in metallurgy, SA allows the occasional “bad” decision early on, which helps it escape local optima. As the “temperature” cools, it becomes more selective, honing in on better solutions. While it’s great for complex landscapes, its computational appetite and reliance on tuning can be challenging.

**Genetic Algorithms (GA)**  
GA is the strategist, mimicking natural selection. It evolves a population of solutions over generations, blending and mutating them until it finds the best. This approach is incredibly robust for multi-modal problems but takes the longest time and demands careful tuning of population size and mutation rates.

---

## **The Challenges: Four Peaks, Max K-Colour, and Neural Networks**

To test these algorithms, I threw two classic optimization puzzles their way—the **Four Peaks problem** and the **Max K-Colour problem**—along with a real-world challenge: training a neural network using the **Wine Quality dataset**.

- **Four Peaks Problem:** A binary string puzzle rewarding balanced patterns of 0s and 1s. A test of exploration versus exploitation.
- **Max K-Colour Problem:** A graph-coloring challenge, aiming to minimize conflicts while using a limited palette.
- **Neural Network Training:** Using randomized optimization to tune weights instead of gradient-based backpropagation.

---

## **The Results Are In!**

### **Four Peaks and Max K-Colour**
- **RHC:** Quickest to finish but struggled with complex problem structures, often settling for local optima.
- **SA:** Balanced performance, excelling in escaping local optima but slowed down by computational demands.
- **GA:** The global optimizer—reliable but slow. Its population diversity made it robust against local minima, though it required more time and effort to fine-tune.

### **Neural Network Training**
When compared to BP:
- **BP:** The reigning champion. Faster and more precise, its gradient-based approach outperformed the randomized trio.
- **RHC and SA:** Comparable accuracy and recall but lagged in precision and F1-scores.
- **GA:** The weakest performer for neural networks, with low efficiency and cost-effectiveness.

---

## **Lessons Learned**

Here’s what my adventure with randomized optimization taught me:
1. **One Size Doesn’t Fit All:** Each algorithm has its sweet spot. RHC is perfect for quick and simple tasks, SA thrives in rugged terrains, and GA excels in highly complex problems.
2. **Tuning Matters:** Parameters like SA’s cooling schedule or GA’s population size can make or break an optimizer’s performance.
3. **Blend and Match:** For real-world problems, combining traditional and randomized techniques might be the smartest approach.

---

## **A Fun Takeaway: No-Free-Lunch for Optimizers**

The **No-Free-Lunch theorem** reminds us that no single optimizer reigns supreme across all problems. It’s a humbling reminder that every algorithm has its quirks, strengths, and limits. The key is to understand the problem you’re tackling and pick the right tool—or tools—for the job.

---

## **Final Thoughts**

Randomized optimization isn’t just a backup for gradient-based methods—it’s a whole toolbox for tackling the kinds of messy, non-differentiable problems we often encounter in the real world. Whether you’re navigating the peaks of a binary puzzle or diving into neural network training, there’s something fascinating about letting randomness guide the way.

---

**Note: If the embedded PDF is not displayed properly or if you are viewing this on a mobile device, <a href="https://kodendaal.github.io/assets/random_optimization.pdf" target="_blank">please click here</a> to access the PDF directly.**

<div id="adobe-dc-view" style="width: 100%;"></div>
<script src="https://acrobatservices.adobe.com/view-sdk/viewer.js"></script>
<script type="text/javascript">
	document.addEventListener("adobe_dc_view_sdk.ready", function(){ 
		var adobeDCView = new AdobeDC.View({clientId: "53fde15a134945fb9a98d2c4b0fe605e", divId: "adobe-dc-view"});
		adobeDCView.previewFile({
			content:{location: {url: "https://kodendaal.github.io/assets/random_optimization.pdf"}},
			metaData:{fileName: "random_optimization.pdf"}
		}, {embedMode: "IN_LINE"});
	});
</script>
