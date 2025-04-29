---
title:  "RL Planning for Traffic Lights and Warehouses"
mathjax: true
layout: post
categories: 
  = github
  - website
---

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/XXX" alt="Asteriods and Wine" style="width: 800px; height: auto;">
</div>


# Stopping for Green: teaching algorithms to tame traffic lights *and* warehouse robots 🚦🤖  

*(A breezy tour of reinforcement-learning experiments that started with “what if?” and ended with **better-behaved intersections and delivery droids**.)*  

---

## 1  Why I suddenly cared about queues and collisions  

Picture this: you’re running late, the light stubbornly stays red, and the only thing moving is your smartwatch’s heart-rate graph. Later, you order something online and—surprise!—it’s delayed because a warehouse robot got lost playing bumper-cars with a forklift.  

Both headaches share a root cause: **sequential decisions under uncertainty**. That’s catnip for reinforcement learning (RL), so I built two toy worlds:

1. **Traffic-Light Town** – one four-way intersection, cars arriving via Poisson magic, one light that can stay put or switch.  
2. **Warehouse-World** – a grid full of boxes, walls, equipment, roaming workers, and one slightly clumsy robot tasked with deliveries.

Each environment is an MDP (state, action, reward, transition, discount). Now we need agents.     

---

## 2  Meet the squad (a.k.a. four ways to adult in an MDP)

| Persona | Algorithm | Elevator pitch |
|---------|-----------|----------------|
| **The Planner** 🗺️ | **Value Iteration** | Looks ahead everywhere, scribbles values on a cosmic whiteboard, then acts. |
| **The Iterative Boss** 🧑‍💼 | **Policy Iteration** | “Here’s the plan… wait, let’s evaluate… okay new plan!”—fewer updates, beefier math. |
| **The Adventurous Teen** 🛹 | **Q-Learning** | Ignores the family plan, learns by trial and error, and still (eventually) finds optimality. |
| **The Cautious Driver** 🚗 | **SARSA** | Sticks to what it actually does, updating on-policy; smoother, safer, sometimes slower. |  

All four share an ε-greedy *“try-stuff-early, exploit-later”* vibe, with exponential decay to keep wanderlust in check.     

---

## 3  Experiment montage (what we tweaked and why)

### Traffic-Light Town  
*E1* Baseline; *E2* **reward-shaping** (bonuses for clearing queues, side-eye for congestion); *E3* early-exit when intersection is empty; *E4* balanced vs skewed traffic arrival rates.

### Warehouse-World  
*E1* Baseline; *E2* reward-shaping (Manhattan-distance candy, collision pain); *E3* four flavours of start/goal randomness; *E4* deterministic ➜ coin-toss action noise.

Same hyper-params unless noted: γ = 0.9, α = 0.1, episodes = 2 000.  

---

## 4  What happened (highlights only—we spared you 40 000 plots)

### 4.1  Traffic results  

* **Reward shaping = green lights galore**. Model-free agents stopped the dreaded *“blink-blink-stall”* pattern and actually **kept queues short**.  
* **Terminal on clearance** made planners laser-focused on short-term wins; model-free lost some steam because episodes ended before long horizons paid off.  
* **Skewed arrivals** (think Monday-morning commute) exposed model-free bias—over-serving the busy lane, starving the quiet one. Planners stayed balanced.  

### 4.2  Warehouse results  

* **Distance-based treats** turned Q-Learning into a speedy courier (≈ 3 boxes/episode) while SARSA chose the *“slow-and-no-crash”* lifestyle.  
* Randomising the goal ballooned the state-space; SARSA froze, Q-Learning bumped into things—but extra training (10 k episodes) revived them.  
* **A pinch of randomness** (80/20 action success) broke deterministic cycling and reduced time-outs; too much chaos (50/50) sent everyone back to square one.  

---

## 5  Hyper-parameter heartbreak (& hope)  

| Knob | Low setting | High setting | Observed mood swing |
|------|-------------|--------------|---------------------|
| γ (discount) | 0.5 | 0.9 | Lower γ loved quick traffic fixes; higher γ needed for epic warehouse treks. |
| θ (planner convergence) | 1e-2 | 1e-10 | Loose tolerance = faster but a bit sloppier value maps. |
| ε decay | 0.5 | 0.99 | Fast decay calmed policies early; slow decay uncovered hidden corners. |
| Episodes | 5 000 | 10 000 | Diminishing returns in Traffic-Town, but a **lifesaver** for lost robots. |     

Moral: tune knobs *per environment*. One size never fits all—just like traffic lights in a warehouse would be silly.

---

## 6  Big take-aways (TL;DR)

1. **Planners** shine when you *know* the rules and crave fast convergence—great for modest intersections.  
2. **Model-free** wins when the map is fuzzy or huge—robots bump into unknowns daily.  
3. **Reward shaping is practically mentorship**: give agents milestone pats on the back and they’ll learn faster (but don’t over-script them).  
4. **A dash of stochasticity prevents loop-lock**—too little = boring cycles, too much = chaos.  
5. **Hyper-parameters are the secret sauce**. Invest in a good taste-test upfront.

---

## 7  Future mischief

* Multi-intersection networks with coordinated lights (think agent gossip).  
* Swarms of robots sharing Q-tables or gossiping via federated learning.  
* Potential-based shaping to guarantee no-regret tweaks.  
* Deep RL for pixel-rich simulations—traffic cams and warehouse CCTV, here we come.

---

*Thanks for reading!* If you’re now imagining courteous traffic and stress-free delivery bots, my work here is done. Feel free to reuse the code, tweak the hyper-params, or just brag at the next coffee break that you know why ε matters.  

Happy learning—and may all your lights be green! 💚

---

**Note: If the embedded PDF is not displayed properly or if you are viewing this on a mobile device, <a href="https://kodendaal.github.io/assets/CS7642_RL___Project_1_final.pdf" target="_blank">please click here</a> to access the PDF directly.**

<div id="adobe-dc-view" style="width: 100%;"></div>
<script src="https://acrobatservices.adobe.com/view-sdk/viewer.js"></script>
<script type="text/javascript">
	document.addEventListener("adobe_dc_view_sdk.ready", function(){ 
		var adobeDCView = new AdobeDC.View({clientId: "03c5f4ff786a46619b7edf7178e35c18", divId: "adobe-dc-view"});
		adobeDCView.previewFile({
			content:{location: {url: "https://kodendaal.github.io/assets/CS7642_RL___Project_1_final.pdf"}},
			metaData:{fileName: "CS7642_RL___Project_1_final"}
		}, {embedMode: "IN_LINE"});
	});
</script>
