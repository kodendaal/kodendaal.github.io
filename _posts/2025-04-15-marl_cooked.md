---
title:  "Whisk It Good or Overcook! Exploring MARL"
mathjax: true
layout: post
categories: 
  = github
  - website
---

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/overcooked.png" alt="Overcooked" style="width: 800px; height: auto;">
</div>

*A romp through multi-agent reinforcement learning that turns chaos into culinary coordination — all while keeping the maths on the menu.*  

---

## Order-up: why Overcooked is RL’s hottest test kitchen  

Picture the scene: two frantic chefs, one cramped galley, onions rolling everywhere, timers beeping, plates vanishing… and *you* only control the learning algorithm. That’s **Overcooked-AI**, a cooperative benchmark where agents must prepare as many three-onion soups as possible within 400 ticks of the game clock. Sparse rewards, tight corridors, and a teammate that can body-block you at every turn — it’s the perfect crucible for **multi-agent reinforcement learning (MARL)**.   

---

## Which recipe did we try?  

| Style | Algorithm | TL;DR |
|-------|-----------|-------|
| **Solo cooks** 👩‍🍳 | **Independent Q-Learning + Double DQN** (IQL-DDQN) | Treat each chef as an island; hope for emergent teamwork. Simple, often clueless. |
| **Co-chef fusion** 🤝 | **Value Decomposition Network + DDQN** (VDN-DDQN) | Train one joint value, slice it into per-chef utilities so they still act locally. Adds collaboration on the cheap. |  

Both run under the classic **centralised training, decentralised execution** mantra: give them the full kitchen map while learning, then cut the radio and let each chef rely only on its own 96-dim observation at test time.   

### Extra spices  

* **Symmetric replay buffer**: store each experience twice, swapping chef A ↔ chef B, which doubles useful data in a perfectly mirrored kitchen.  
* **Reward shaping**: tiny tips for onion-in-pot (+3), dish pick-up (+1), soup pick-up (+5) — on top of the big +20 for a served bowl. Keeps gradients alive.  
* **Curriculum**: start in the tiny **Cramped Room**, graduate to **Coordination Ring**, then tackle the beastly **Counter Circuit**.   

---

## Prep work — training at a glance  

* **Optimiser**: DDQN with target-network soft updates (τ ≈ 2-3).  
* **Batch**: 1 024 (big bites keep gradients smooth).  
* **ε-greedy**: linear decay from 1 → 0.1 by 80 % of training, tiny 0.05 jitter at evaluation.  
* **Episodes**: 1 000 / 2 500 / 5 000 for the three layouts, plus Optuna sweeps (10 trials) to lock hyper-params.   

---

## Results — how many bowls did we ladle?  

| Layout | Benchmark = 7 soups | IQL-DDQN | VDN-DDQN | Curriculum (VDN) |
|--------|--------------------|----------|----------|-------------------|
| Cramped Room | ✓ | 3 | **12** | — |
| Coordination Ring | ✓ | 0 | **14** | — |
| Counter Circuit | ✗ | 0 | 0 | **7** |

* In small & medium kitchens, **VDN crushed the benchmark**, proving that a shared value table makes chefs stop bumping and start batching onions.  
* In the labyrinthine Counter Circuit, both methods face-planted — until we **boot-strapped from a simpler level**. Curriculum trimmed learning from 5 000 futile episodes to **~1 100** productive ones.   

---

### Ablation quick-fire 🔍  

| Toggle | Outcome |
|--------|---------|
| **Reward shaping OFF** | Agents starved: no gradient, no soups. |
| **Symmetric buffer OFF** | -30 % servings; sample efficiency tanked. |
| **DDQN → vanilla DQN** | No big change in Cramped Room (low stochasticity). Expect bigger wins in messier kitchens. |   

---

## What we learned (besides julienning onions)

1. **Credit assignment is king** — VDN’s additive trick is cheap yet powerful for tightly-coupled tasks.  
2. **Reward shaping must be Goldilocks** — too little and you starve, too much and agents farm onions forever without serving.  
3. **Symmetry is free lunch** — mirror every trajectory and your replay buffer suddenly sees twice the angles.  
4. **Curriculum beats brute force** — let chefs learn footwork in a tiny galley before throwing them into the Costco kitchen.  
5. **Complex layouts still hurt** — for true mastery we’ll likely need QMIX, MAPPO or distributional tricks.   

---

## Next courses  

* **Non-linear mixers** (QMIX) to model “you chop, I stir” dependencies.  
* **Prioritised + n-step replay** for snappier credit propagation.  
* **Potential-based shaping** that rewards proximity to *future* soup deliveries, not just onions-in-pot.  
* **Longer training & randomised layouts** to nix over-fitting.  

---

## Final plate-up  

> *“Great kitchens run on rhythm. Great MARL agents learn that rhythm by sharing credit, replaying symmetry, and never forgetting to stir the pot.”*  

With a pinch of decomposition and a dash of curriculum, our twin neural chefs now crank out onion soup like a well-oiled diner. Lunch rush conquered — time to teach them soufflés. Bon appétit, RL enthusiasts!

---

**Note: If the embedded PDF is not displayed properly or if you are viewing this on a mobile device, <a href="https://kodendaal.github.io/assets/CS7642_RL___Project_3_final.pdf" target="_blank">please click here</a> to access the PDF directly.**

<div id="adobe-dc-view" style="width: 100%;"></div>
<script src="https://acrobatservices.adobe.com/view-sdk/viewer.js"></script>
<script type="text/javascript">
	document.addEventListener("adobe_dc_view_sdk.ready", function(){ 
		var adobeDCView = new AdobeDC.View({clientId: "68b5f3c3d85c4899b9d64db2ada1f842", divId: "adobe-dc-view"});
		adobeDCView.previewFile({
			content:{location: {url: "https://kodendaal.github.io/assets/CS7642_RL___Project_3_final.pdf"}},
			metaData:{fileName: "CS7642_RL___Project_3_final"}
		}, {embedMode: "IN_LINE"});
	});
</script>
