---
title:  "Fast Lap? Going for Pole using RL"
mathjax: true
layout: post
categories: 
  = github
  - website
---

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/deepracer.png" alt="deepracer" style="width: 800px; height: auto;">
</div>


*Spoiler: teaching a 1/18-scale race-car to zoom round three tracks is easier than convincing it to dodge six traffic cones—or three pesky rivals.*

---

## Start your (simulated) engines

AWS **DeepRacer** is a cute little RC car with a GPU onboard and a massive cloud simulator behind it. In the sim, each “timestep” is a still from twin 160 × 120 greyscale cameras plus a 64-beam LiDAR snapshot—all you get to decide is which discrete *steering × throttle* combo to fling back at the physics engine.

We set out to answer one question:

> **Can one policy lap three very-different circuits and *still* cope with cones and competitors—if we just reward-shape wisely and press “train”?**&#x20;

---

## The three test-benches

| Track (easy → evil) | Length × Width      | Nickname           | Gotchas                        |
| ------------------- | ------------------- | ------------------ | ------------------------------ |
| **A–Z Speedway**    | 16.6 m × 1.07 m     | “Wide & Mild”      | Baby curves, plenty of run-off |
| **Smile Speedway**  | 23.1 m × 1.07 m     | “Medium Smirk”     | Chicanes just for fun          |
| **Empire City**     | 21.9 m × **0.76 m** | “Narrow Nightmare” | Tall walls, blind exits        |

Each circuit is driven in three modes:

1. **Time-Trial** — clean lap, no hazards.
2. **Obstacle** — six static barrels in awkward spots.
3. **Head-to-Bot** — three unpredictable robot rivals.

Total = **nine** distinct challenges.

---

## Training recipe (PPO à la carte)

* **Algorithm**: *Clipped* Proximal Policy Optimisation—stable, on-policy, works nicely with discrete action lattices.
* **Network**:

  * *CNN* (3 × conv) ⟶ 11 k-dim visual code.
  * *MLP* on LiDAR ⟶ 128-dim spatial sniff.
  * Fuse, compress to 512, then **actor / critic** heads.
* **Curriculum**:

  1. Fixed start on wide track.
  2. Random start poses.
  3. Random direction + harder, narrower tracks.
* **Timesteps**: 20 k (≈ 2 h sim time—hey, cloud credits are finite!).&#x20;

### Reward cocktail

$$
R = R_\text{center} + R_\text{progress} + R_\text{align} - R_\text{obstacle} - 10\;\mathbf 1_\text{crash}
$$

* **Centerline hugging:** Gaussian drop-off.
* **Progress drip:** +1 per % distance.
* **Lap bonus:** scaled to reward speed.
* **Obstacle cone of pain:** exponential if LiDAR < 1 m.

Weights = 1.0 each (heuristic—but worked okay for solo laps).&#x20;

---

## Qualifying results

| Scenario                   | A–Z Speedway | Smile Speedway | Empire City |
| -------------------------- | ------------ | -------------- | ----------- |
| **Time-Trial** completion  | **100 %**    | **100 %**      | **97 %**    |
| **Obstacle** completion    | 75 %         | 55 %           | 38 %        |
| **Head-to-Bot** completion | 50 %         | 27 %           | 4 %         |

*Lap times (successful runs):* 9 s ➜ 15 s ➜ 18 s in solo mode; add \~+10 s when barrels appear.

### TL;DR

* Curriculum nailed lane-keeping on all geometries.
* One static cone = sudden amnesia: the car slams brakes, weaves, or just punts the barrel.
* Three bots = utter panic on narrow track; success nearly zero.&#x20;

---

## Post-race debrief — what went sideways?

1. **Training / evaluation mismatch**
   *We never showed obstacles or rivals during training*, so LiDAR never mattered. Domain shift = wipe-out.

2. **Reward conflicts**
   Centerline bonus fights obstacle penalty (“should I swerve off-centre or stay put?”). Without clever weighting, the agent dithers.

3. **Short budget & vanilla hyper-params**
   20 k steps is peanuts for vision + liDAR PPO. More epochs & Optuna sweeps could squeeze extra generalisation.

4. **Single-agent mindset**
   Head-to-bot is a *multi-agent* game; PPO with single-agent POMDP assumptions can’t reason about opponent intent.

---

## Lessons served hot

| Take-away                                                    | Why it matters                                                                |
| ------------------------------------------------------------ | ----------------------------------------------------------------------------- |
| **Curricula need *task* diversity, not only map diversity.** | Track randomisation worked; hazard types didn’t.                              |
| **Reward shaping is a double-edged steering wheel.**         | Dense signals speed learning but may encourage “centerline or bust” fixation. |
| **LiDAR without practice ≈ dashboard ornament.**             | Sensory fusion only helps if training exposes the relevant stimuli.           |
| **Multi-agent scenarios demand CTDE or self-play.**          | Without it, bots are unpredictable ghosts.                                    |

---

## Next pit-stops

* **Inject obstacles & bots into curriculum.** Maybe alternate hazard-heavy episodes with clean laps.
* **Simplify reward: progress + crash penalty**; let agent discover lane preference.
* **CTDE PPO + opponent modelling** — predict rival trajectories, plan overtakes.
* **Longer runs & automated hyper-param search** (Optuna).
* **Heavy domain randomisation** (textures, physics) for sim-to-real dreams.

---

## Chequered flag

We built a DeepRacer that blitzes solo laps on three very different circuits—proof that PPO plus a thoughtfully staged curriculum can squeeze general driving skills out of pixel soup. But toss a cone or a competitor on track and the gap shows: *generalisation is a much tougher corner than it looks on the map*. Time to tweak the curriculum, rethink rewards, and maybe give our little racer some social-driving lessons.

Until then, keep it centered, keep it fast—and don’t forget to look *two waypoints* ahead! 🏁

---

**Note: If the embedded PDF is not displayed properly or if you are viewing this on a mobile device, <a href="https://kodendaal.github.io/assets/CS7642_RL___Project_4_final.pdf" target="_blank">please click here</a> to access the PDF directly.**

<div id="adobe-dc-view" style="width: 100%;"></div>
<script src="https://acrobatservices.adobe.com/view-sdk/viewer.js"></script>
<script type="text/javascript">
	document.addEventListener("adobe_dc_view_sdk.ready", function(){ 
		var adobeDCView = new AdobeDC.View({clientId: "f737bdc1a7c441cdab7237b8f5ac89f7", divId: "adobe-dc-view"});
		adobeDCView.previewFile({
			content:{location: {url: "https://kodendaal.github.io/assets/CS7642_RL___Project_4_final.pdf"}},
			metaData:{fileName: "CS7642_RL___Project_4_final"}
		}, {embedMode: "IN_LINE"});
	});
</script>
