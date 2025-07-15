
## Teaching an Old Ship New Tricks: Taming Wave-Induced Roll with Deep Reinforcement Learning

The gentle rocking of a boat can be a soothing lullaby. But when that gentle rock turns into a violent, unpredictable roll, it’s anything but. For centuries, naval architects have worked to counteract this roll, especially when a ship is at its most vulnerable—at anchor, with no forward speed to aid stability. Traditional solutions like stabilization fins work well, but what if we could make them *smarter*? What if a ship’s control system could learn, adapt, and react to the waves with the intuition of a seasoned sailor?

This is the story of how we took on that challenge. We're going to take a deep dive into the world of artificial intelligence to show you how we trained an AI agent, from scratch, to master the complex art of ship roll stabilization. Forget everything you know about manually tuned controllers; we’re entering the era of data-driven, self-learning systems. This is our journey into the heart of Deep Reinforcement Learning (RL).

### Step 1: Building a Digital Ocean - Our Simulation Playground

You don’t teach an AI to swim by throwing it into the ocean. You build it a world-class digital swimming pool first. It’s simply not feasible (or safe!) to train an RL agent on a real multi-million dollar yacht. We needed a robust, high-fidelity simulation environment where our agent could experiment, fail, and learn millions of times over without consequence.

We developed a custom environment, compatible with the industry-standard OpenAI Gym, that accurately emulates the roll dynamics of a ship. This became the playground for our RL agent. The interaction is a continuous loop, a dialogue between the "Agent" (the AI brain) and the "Environment" (the simulated ship).

<br>
<p align="center">
    <img src="https://storage.googleapis.com/agentops-images/b77c44e9-11c2-4091-a67b-b384d5dfeb2f.png" width="400">
    <br>
    <em><b>Fig. 2-3:</b> A schematic diagram of the reinforcement learning process.</em>
</p>
<br>

At every time step (in our case, every 0.25 seconds), this dialogue unfolds:
1.  **Observation:** The Environment tells the Agent what's happening. This isn't just a single number; it's a vector of crucial data:
    `ot = [Φ, Φ_dot, δ, δact]T`
    *   `Φ`: The current roll angle of the ship.
    *   `Φ_dot`: The current roll rate (how fast it's rolling).
    *   `δ`: The fin's angular acceleration.
    *   `δact`: The actual, current angle of the stabilization fin.
2.  **Action:** Based on this observation, the Agent makes a decision: what should the new target angle for the fins be?
3.  **Reward:** The Environment responds with a scalar "reward" signal. This is the critical feedback. A positive reward says, "Good job!" A negative one says, "That wasn't helpful." This feedback guides the entire learning process.

To make the challenge realistic, we imposed physical limits, just as a real fin system would have.

**Table 2-1: Observation and action limits used in the RL workflow.**
| Symbol | Physical meaning | Range |
| :--- | :--- | :--- |
| Φ | Roll angle [rad] | [-60°, +60°] |
| Φ_dot | Roll rate [rad s⁻¹] | [-2π, +2π] |
| δ | Fin angular accel. [rad s⁻²] | [-60°, +60°] |
| δact | Actual fin angle [rad] | [-30°, +30°] |
| at | Commanded fin angle [rad] | [-30°, +30°] |

### Step 2: The Brains of the Operation - Our Soft Actor-Critic (SAC) Agent

With our digital ocean ready, we needed an AI "brain" to navigate it. We chose a powerful, state-of-the-art RL algorithm called **Soft Actor-Critic (SAC)**. Here’s why SAC was the perfect candidate:
*   **Model-Free:** It doesn’t need a perfect mathematical model of ship physics to work. It learns directly from the data it gathers.
*   **Data-Driven & Efficient:** It’s known for being highly sample-efficient, meaning it can learn effective strategies without an exorbitant amount of data.
*   **Built-in Exploration:** SAC has a unique feature—an "entropy bonus." In simple terms, it not only tries to get the highest reward but also actively seeks to be as exploratory as possible. This prevents it from getting stuck in a rut with a sub-optimal strategy and encourages it to discover more robust and effective solutions.

At its core, the agent is trying to solve the following optimization problem, which elegantly balances maximizing rewards with encouraging exploration:
<br>
<p align="center">
    <img src="https://storage.googleapis.com/agentops-images/3430c5e7-a979-4ac9-8a8b-3e5f4124016c.png">
</p>
<br>

The agent itself is composed of neural networks. Here’s a peek at the architecture of its "brain."

**Table 2-2— Neural-network architecture for actor and twin critics.**
| Layer | Size | Activation |
| :--- | :--- | :--- |
| Input | 4 | |
| Hidden 1 | 128 | tanh |
| Hidden 2 | 128 | tanh |
| Actor outputs | μ, log σ (dim =\|A\|) | linear |
| Critic outputs | Q-value (scalar) | linear |

### Step 3: The Curriculum - How to Teach an Agent to Tame the Sea

Having a brain and a playground isn't enough. You need a curriculum. For an RL agent, the curriculum is defined by two things: the reward function and the training regimen.

#### The Reward: Defining "Good"
The reward function is the most critical piece of the puzzle. It’s how we communicate our goal to the agent. A poorly designed reward can lead to bizarre, unintended behaviors. Our goal is simple: stable and efficient roll damping. We translated this into a mathematical formula:
<br>
<p align="center">
    <img src="https://storage.googleapis.com/agentops-images/7f4ef289-43c7-4389-9b62-6c2e88a3e758.png">
</p>
<br>
This function explicitly penalizes two things: the residual roll angle (`Φ`) and the roll rate (`Φ_dot`). In short, we reward the agent for keeping the ship as still as possible.

#### The Regimen: Domain Randomization
We don't want an agent that is a one-trick pony, only capable of handling a single, specific wave pattern. We want a robust, seasoned sailor that can handle a variety of sea conditions. To achieve this, we used **Domain Randomization**.

Instead of training our agent on a single, fixed sea state, we subjected it to a wide and constantly changing variety of conditions at the start of every training episode.

**Table 2-3—Domain-randomisation envelope for sea-state parameters.**
| Parameter | Min | Max |
| :--- | :--- | :--- |
| Hs (significant height) | 0.5 m | 2.0 m |
| Tp (peak period) | 8 s | 12 s |
| Heading (relative) | 90° | 90° |
| Wave seed | 0 | 10⁶ |

This process forces the agent to learn a generalized policy that is effective across a whole family of sea states, making it incredibly resilient.

We also employed a multi-stage training pipeline, starting simple and gradually increasing the complexity to ensure stable and efficient learning.

<br>
<p align="center">
    <img src="https://storage.googleapis.com/agentops-images/a4d0f62b-65c8-47a3-b09e-ddb890881be8.png" width="500">
    <br>
    <em><b>Fig 3-4:</b> The multi-stage training pipeline.</em>
</p>
<br>

### Step 4: Graduation Day - The Results

After countless hours of simulation and training, did our AI agent learn its lessons? The results were fascinating. The training curves below show a clear story: the agent steadily improved its performance, reducing the ship's roll and maximizing its cumulative reward over time.

<br>
<p align="center">
    <img src="https://storage.googleapis.com/agentops-images/4bb8421d-9e6e-473d-82d2-28c9480a4739.png" width="600">
    <br>
    <em><b>Figure XX:</b> Training process key indicators: (a) Roll RMS, (b) % Roll Reduction (active vs passive), and (c) Cumulative Mean Reward. The "random" agent is our robust, domain-randomized agent.</em>
</p>
<br>

The time-series plots below give a dramatic visual of the agent's success. On the left is the "specialist" agent trained on a single wave pattern; on the right is our robust "generalist" agent. Both significantly suppress the roll compared to the uncontrolled "passive" state.

<br>
<p align="center">
    <img src="https://storage.googleapis.com/agentops-images/61c40215-6449-41d5-9271-41716da65860.png" width="800">
    <br>
    <em><b>Figure XX:</b> Time-trace comparison using beam seas with Hs = 1.5 m, Tp = 10 s and 500s: (a) Single-wave agent and (b) Random-domain Agent. The blue line (RL Roll) shows the dramatic reduction compared to the uncontrolled red line (Passive Roll).</em>
</p>
<br>

#### Sample Efficiency and Final Performance

A key metric in RL is "sample efficiency"—how much data is needed to learn? The graph below plots performance against training time. We compared our RL agents against a conventional Saturated PD (SPD) controller. While the SPD controller finds its optimal settings faster, the RL agents learn a complex, non-linear control policy entirely from scratch.

<br>
<p align="center">
    <img src="https://storage.googleapis.com/agentops-images/ac5eb507-6815-46e3-abcf-5f93933c46d3.png" width="800">
    <br>
    <em><b>Figure XX:</b> Sample efficiency showing roll reduction vs. training data. The chart shows performance on waves of a) 1.5m, b) 0.5m, and c) 2.5m. Our RL agents (single wave and multiple waves) show a clear learning trajectory.</em>
</p>
<br>

The final numbers speak for themselves. In the most challenging sea states, the robust, multi-wave RL agent even outperformed the specialist agent, proving the power of domain randomization.

**Table XX: Final roll reduction**
| Wave height | RL single wave | RL multiple waves |
| :--- | :--- | :--- |
| 0.5 m | 84% | 81% |
| 1.5 m | 52% | 55% |
| 2.5 m | 22% | 28% |

### The Future is Adaptive

This project proved that Reinforcement Learning has immense potential. We successfully trained an AI agent to master a complex, real-world control task. While conventional controllers still hold an edge in tuning speed, the path forward is clear.

Our next steps are to push the boundaries even further:
*   **Give the Agent a Memory:** Implement advanced network architectures like LSTMs that can recognize long-term wave patterns, much like a human sailor.
*   **Expand its Senses:** Feed the agent more data, like heave and pitch motion, so it can anticipate coupled motions and react more intelligently.
*   **The Hybrid Approach:** The ultimate goal may not be to replace classical controllers, but to augment them. Imagine a system where a proven controller handles the basics, and an RL agent learns to provide small, intelligent corrections on top. This offers the best of both worlds: the reliability of classical control and the adaptive power of AI.

We are just scratching the surface of what is possible when we combine centuries of naval engineering with the cutting edge of artificial intelligence. The future of ship control is not just automated; it's adaptive, intelligent, and continuously learning.
