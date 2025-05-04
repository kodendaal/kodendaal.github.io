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

*A light-hearted tour of my AWS DeepRacer reinforcement-learning project*

---

## Warm-up Lap — Why race toy cars with RL?

If you can teach a 1 / 18-scale racer to hug corners, dodge cones and out-smart rival bots, you’ve basically distilled every juicy challenge in autonomous driving into a bite-size sandbox. AWS DeepRacer gives us that sandbox: simulated tracks, stereo cameras, a LIDAR ring and just enough physics to make you fist-pump when the car finishes a lap cleanly. My mission? Train **one** brain that blasts around three tracks *and* survives three very different race modes—solo time-trials, static-obstacle slaloms and chaotic head-to-head heats—without rage-quitting into a wall.&#x20;

---

## Meet the Pit-Crew Algorithms

### Proximal Policy Optimization (PPO)—the steady race engineer

I picked **PPO (clipped)** because it updates the policy in baby steps—like tightening wheel-nuts a quarter-turn at a time instead of yanking them off. The clipped objective keeps the new policy from wandering too far from the safe baseline, which is gold when every bad update sends your car lawn-mowing.&#x20;

### A camera-LIDAR dream team

The agent sees the world through a **3-layer CNN** that chews on twin 160 × 120 grayscale images, while a mini-MLP digests a 64-ray LIDAR scan. Mash those together, pass through a 512-unit “combiner,” and you have a fused ego-view that feeds both actor (which button to press) and critic (was that smart?).&#x20;

---

## Track Walk & Scenarios

| Track nickname     | Real name          | Width  | Personality                      |
| ------------------ | ------------------ | ------ | -------------------------------- |
| **A-Z Speedway**   | reInvent2019 Wide  | 1.07 m | Friendly oval for first dates    |
| **Smile Speedway** | reInvent2019 Track | 1.07 m | Twisty grin-shaped sprint        |
| **Empire City**    | New York Track     | 0.76 m | Skinny, skyscraper-tight corners |

Each track is tackled in three flavors:

1. **Time-Trial** – no traffic, just vibes
2. **Obstacle-Avoidance** – six static barrels begging for bumper kisses
3. **Head-to-Bot** – three rambunctious opponent cars that never heard of personal space&#x20;

---

## Reward Shaping — bribing the driver

Think of rewards as snacks you toss at the car to encourage good manners:

* **Stay centered:** exponential bonus for keeping your wheels near the mid-line
* **Make progress:** a linear treat every time you inch forward
* **Celebrate the finish:** big cookie for ≥ 98 % progress, scaled by how few steps you used
* **Fear the barrel:** exponential penalty when LIDAR screams “too close!”
* **Crash tax:** -10 if you smack a wall; +20 if you see the chequered flag

Weights? One-third each to center, progress and obstacle penalties—because democracy.&#x20;

---

## Training Regimen — from baby steps to Nürburgring

1. **Fixed start on A-Z** – learn to drive in a straight line without crying.
2. **Random starts** – spawn the agent anywhere on the track so it can’t memorise scenery.
3. **Random direction + harder tracks** – reverse laps and graduate to the slim-fit Empire City.

Twenty-thousand simulation steps (\~2 hours on a plain laptop) with PPO hyper-params straight from the OpenAI cookbook (γ = 0.99, ε = 0.2, 5 epochs per 512-step rollout).&#x20;

---

## Race-Day Results

### Time-Trials: **Flawless victory**

* 100 % lap completion on all tracks
* Lap times: **92 s** (A-Z), **302 s** (Smile), **431 s** (Empire)

### Obstacle slalom: **Traffic-cone trauma**

* Completion plummets to **15–22 %**. The car either tip-toes till timeout or swerves into the wall after a heroic dodge.

### Head-to-Head: **Bumper-car chaos**

* Completion: **\~50–60 %** on the roomy tracks, nosedives to **≈30 %** on skinny Empire City. Opponent body-checks are brutal.

Moral: Our solo-racing prodigy panics when the playground gets crowded.&#x20;


<div style="text-align: center; margin: 20px;">
  <video style="width: 100%; max-width: 100%; height: auto;" controls>
    <source src="http://kodendaal.github.io/assets/REINVE~1.MP4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
</div>


<div style="text-align: center; margin: 20px;">
  <video style="width: 100%; max-width: 100%; height: auto;" controls>
    <source src="http://kodendaal.github.io/assets/NEW_YO~1.MP4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
</div>


<div style="text-align: center; margin: 20px;">
  <video style="width: 100%; max-width: 100%; height: auto;" controls>
    <source src="http://kodendaal.github.io/assets/NEW_YO~1.MP4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
</div>



---

## Lessons from the Crash Logs

* **Curriculum blind spot:** Training never showed the agent a single cone or rival, so evaluation felt like throwing a toddler onto the Autobahn.
* **Reward tug-of-war:** “Stay centered” vs. “swerve to live” sends mixed signals; weight tuning is black-art territory.
* **Tiny data diet:** 20 k steps are plenty for smooth solo laps but peanuts for learning 4-D chess with moving bots.&#x20;

---

## Next Upgrades

1. **Multi-task curriculum** – sprinkle obstacles and bots *during* training; maybe even self-play.
2. **Lean rewards** – axe the micromanagement; reward progress & penalize collisions, let the network figure out the jazz steps.
3. **Opponent modelling** – give the car a crystal ball (recurrent net) to guess rival moves.
4. **More track time & hyper-tuning** – because GPUs don’t need sleep.&#x20;

---

## Checkered Flag

We turned a timid toy into a track-lapping champ—*as long as nobody else shows up*. The project proves that curriculum learning plus PPO can nail geometry generalization, yet true robustness demands training that mirrors real-world mayhem. Next season, the car’s getting street-smarts, thicker skin and maybe a flamenco horn for overtakes. Stay tuned! 🏁


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
