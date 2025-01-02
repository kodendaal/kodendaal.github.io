---
title:  "Simplifying Ship Design: A Fun Dive into Hull Strength Analysis"
mathjax: true
layout: post
categories: 
  = github
  - website
---

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/ship_long_logo.png" alt="Ship Longitudinal Strength" style="width: 800px; height: auto;">
</div>

Ever wonder what keeps a massive ship from snapping in two while it cruises through the ocean? Turns out, it’s all about **longitudinal strength**—the backbone of a ship’s structural integrity. In my independent research project, I set out to tackle one of the toughest challenges in ship design: streamlining the process of calculating this critical strength without sacrificing accuracy. And yes, it was as exciting as it sounds!

---

### The Problem: Weighty Calculations

Calculating longitudinal strength isn’t a walk in the park. Imagine painstakingly inputting **up to 5000 individual weight items** just to figure out a ship’s weight distribution. It’s a tedious, time-consuming task, but absolutely essential for ensuring the ship won’t fracture or sink. My goal? To make this process faster and smarter without compromising accuracy.

---

### The Approach: Testing Weight Distribution Techniques

I focused on three weight distribution techniques and tested their impact on **still water shear force** and **bending moment**—two key parameters in hull strength. Here’s what I explored:
1. **Parabolic Approximation**: Quick but didn’t pass the accuracy test.
2. **Point-Wise Grouping**: A great choice for academics with better weight input control but slightly lower accuracy.
3. **Trapezoidal Direct Method**: The rockstar of the study with the best accuracy (0.22% and 0.35% improvements for shear and bending moments, respectively).

Using a **local one-at-a-time sensitivity analysis**, I dived deep into how each method performed under different scenarios.

---

### The Big Find: Faster and Smarter Design

Here’s where the magic happened. By simplifying weight distribution:
- I cut **input time by nearly 30%!**
- Two real-world vessel studies showed additional **time savings of 24.97% and 27%**.
- Accuracy? The differences from fully detailed cases were minor, between **0.3% and 2.3%**, well within acceptable limits.

What does this mean? You don’t need to model every tiny detail to get reliable results. Smarter grouping and streamlined methods can save both time and resources.

---

### Why It Matters

This research proves that efficient weight distribution techniques can revolutionize ship design:
- **Faster Calculations**: Time saved can be redirected to other critical design tasks.
- **Enhanced Accuracy**: Even simplified methods deliver reliable results.
- **Resource Savings**: Less time and effort mean lower costs and greater efficiency.

---

### A Look Ahead

With these findings, shipbuilders and designers have the tools to make the engineering process smoother, faster, and just as reliable. Who knows? The next big yacht might just owe its sleek design to a more efficient weight input process!

In the end, it’s all about making ship design less about the grunt work and more about innovation—and that’s something to celebrate. 🚢✨

---

**Note: If the embedded PDF is not displayed properly or if you are viewing this on a mobile device, <a href="https://kodendaal.github.io/assets/project_independent.pdf" target="_blank">please click here</a> to access the PDF directly.**

<div id="adobe-dc-view" style="width: 100%;"></div>
<script src="https://acrobatservices.adobe.com/view-sdk/viewer.js"></script>
<script type="text/javascript">
	document.addEventListener("adobe_dc_view_sdk.ready", function(){ 
		var adobeDCView = new AdobeDC.View({clientId: "39900242628d43fcb69e35da520d8db8", divId: "adobe-dc-view"});
		adobeDCView.previewFile({
			content:{location: {url: "https://kodendaal.github.io/assets/project_independent.pdf"}},
			metaData:{fileName: "project_independent.pdf"}
		}, {embedMode: "IN_LINE"});
	});
</script>
