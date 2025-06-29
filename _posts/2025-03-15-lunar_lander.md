---
title:  "Stick the Landing: Continuous-Action RL Meets the Moon"
mathjax: true
layout: post
categories: 
  = github
  - website
---

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/lunar_lander.png" alt="Lunar Lander" style="width: 800px; height: auto;">
</div>

*A chronicle of how one small step for hyper-parameters became a giant leap for continuous-action control.*

---

## What’s harder than parallel parking in traffic?  
Landing a moon-lander with **throttle values that slide, not click**. In the Lunar Lander-Continuous environment you steer two thrusters—main and side—each able to fire anywhere between −1 and +1. Infinite actions, unforgiving physics, and exactly **zero parking sensors**.   

### Why classic Q-learning sulks here  
Deep Q-Networks shine when you can simply say “action #3,” but asking them to sweep an *infinite* action set would melt your GPU. We need a policy that *outputs* real-valued thrust directly. Enter **policy-gradient actor–critic land**!   

---

## Meet today’s hero: Deep Deterministic Policy Gradient (DDPG)  
Think of DDPG as two neural-network buddies:  

| Role | Job | Fun twist |
|------|-----|-----------|
| **Actor** | Decides: “Fire main at 0.42, side at –0.08.” | Gets exploratory jitters from Gaussian noise. |
| **Critic** | Judges that move’s long-term value. | Uses a slowly moving *target* twin to stay chill. |

Both share an experience-replay scrapbook so they don’t overreact to any single bumpy touchdown.   

**Exploration hack:** Instead of the fancy Ornstein-Uhlenbeck process, we simply sprinkled zero-mean Gaussian noise on every thrust command—less tuning, same lunar chaos.   

---

## Rocket science, but reproducible  
* Training: 1 000 episodes × 1 000 steps max, ~1 h on a humble 4-core CPU.  
* Networks: 2 hidden layers, 256 neurons each, ReLU everywhere except a *tanh* at the actor’s output to keep actions in [−1, 1].  
* Lifesavers: gradient clipping (±5) after a few wild loss spikes.   

---

## First light: the baseline launch log  
Early episodes looked like *SpaceX prototypes*: spectacular hops, frequent explosions, reward graph doing the samba. But by episode ~800 the curve flirted with the “mission-success” line of **200 points average**. Default settings finally landed at **≈ 249 ± 57** on the last run—mission technically accomplished!   


<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/lunar_lander_ddpg_clip_fail.gif" alt="lunar fails" style="width: 800px; height: auto;">
</div>

---

## Turbo-tuning with Optuna  
Four knobs went into the Bayesian blender:

1. **Discount γ** (0.90 – 0.99)  
2. **Soft target τ** (0.0001 – 0.01)  
3. **Batch size** {32, 64, 128}  
4. **Update frequency** {1 – 5 actor/critic steps per env step}   

### Surprise winners  
* **γ ≈ 0.985**—big-picture thinking pays off, but γ > 0.99 made the agent dreamy and slow.  
* **τ ≈ 0.0045**—fast enough to learn, slow enough to stay zen.  
* **Batch 128**—more samples, smoother gradients, no memory drama.  
* **Updates every 2-4 steps**—too eager and you chase noise; too lazy and you stagnate.   

Best trial (call sign **T-4**) cruised to **264 ± 23** with steadier landings and smaller variances. Not bad for 20 tries!   

*(Fun fact: a hand-coded PID heuristic still scored ~290, proving that humans with equations can out-fly RL—**for now**.)*  


<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/lunar_lander_ddpg_clip_good.gif" alt="lunar fails" style="width: 800px; height: auto;">
</div>

---

## What nearly cratered us  

| Oops moment | Quick fix |
|-------------|-----------|
| Critic loss skyrocketed → actor followed bad advice | Gradient clipping ±5 |
| Vanishing actor gradients (tanh saturation) | Considering Leaky ReLU next round |
| Critic over-estimates Q (DDPG classic flaw) | TD3 beckons on the roadmap |   

---

## Lessons from low lunar orbit  

1. **Continuous action ≠ chaos** when you hand the wheel to an actor network.  
2. **Noise still matters**—Gaussian simplicity worked fine.  
3. **Hyper-parameters are rocket fuel**; a tiny τ tweak can nosedive or sky-rocket performance.  
4. **Baseline DDPG is good—but TD3, SAC, or PPO could push beyond heuristic pilots.**   

---

## Final transmission  

> *“It’s not just about landing softly; it’s about landing softly **every** time.”*  

DDPG—with a dash of Optuna pixie dust—does exactly that. Next mission: slap entropy bonuses on a Soft Actor-Critic and see if we can beat the human PID wiz. But for tonight, enjoy the view: our neural network just left the lander upright, engines off, and flags flying. 🌔✨  

---

**Note: If the embedded PDF is not displayed properly or if you are viewing this on a mobile device, <a href="https://kodendaal.github.io/assets/CS7642_RL___Project_2_final.pdf" target="_blank">please click here</a> to access the PDF directly.**

<div id="adobe-dc-view" style="width: 100%;"></div>
<script src="https://acrobatservices.adobe.com/view-sdk/viewer.js"></script>
<script type="text/javascript">
	document.addEventListener("adobe_dc_view_sdk.ready", function(){ 
		var adobeDCView = new AdobeDC.View({clientId: "a44769aae36f49c698c67b80c801a81e", divId: "adobe-dc-view"});
		adobeDCView.previewFile({
			content:{location: {url: "https://kodendaal.github.io/assets/CS7642_RL___Project_2_final.pdf"}},
			metaData:{fileName: "CS7642_RL___Project_2_final"}
		}, {embedMode: "IN_LINE"});
	});
</script>
