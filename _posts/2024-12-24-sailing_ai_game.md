---
title:  "Sailing into the Unknown: Building a Regatta Game with AI"
mathjax: true
layout: post
categories: 
  = github
  - website
---

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/sailing_game_logo1.png" alt="Sailing Game" style="width: 800px; height: auto;">
</div>


Creating a game is like setting sail into uncharted waters—a mix of excitement, learning, and overcoming challenges. My latest project, a **sailing regatta game**, combines the thrill of racing with the ingenuity of artificial intelligence (AI). Players take control of a nimble virtual sailboat and compete against a Reinforcement Learning (RL) agent that learns to master the art of sailing.

This blog chronicles the journey of building this game—from basic boat physics to crafting a competitive AI opponent. Whether you're a developer, gamer, or sailing enthusiast, I hope this gives you a glimpse of the creativity and problem-solving behind the scenes.

---

## The Concept: Humans vs. AI on the High Seas

The game’s premise is simple yet engaging:
- **The Goal**: Reach waypoints on a course faster than your opponent.
- **The Twist**: Your opponent is an RL-trained AI capable of adapting its strategies.

The human player controls their boat’s rudder and sails, navigating around waypoints while managing the effects of wind and physics. Meanwhile, the AI agent uses its training to adjust its heading and sails for maximum efficiency.

---

## The Journey: From Concept to Code

### Step 1: Core Game Mechanics
The foundation of the game lies in its mechanics. Sailing involves more than just moving from point A to B; it’s about understanding wind angles, optimizing sail trim, and maneuvering effectively. I started with:

- **Physics Modeling**: Simulating the effects of wind, sail angles, and boat turning.
- **Waypoint Navigation**: Placing waypoints on the course that both the player and AI must navigate around.
- **Basic Controls**: Allowing the human player to adjust the rudder and sails via keyboard inputs.

<div style="text-align: center; margin: 20px;">
  <video max-width: 100%; height: auto; controls>
    <source src="http://kodendaal.github.io/assets/sailing_video_v1.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
</div>

### Step 2: Introducing the AI
Building the AI opponent was a fascinating challenge. Using Python’s **Stable Baselines3** library, I:

- **Created a Gym Environment**: Representing the boat’s state (position, heading, speed) and allowing the agent to take continuous actions like steering and trimming sails.
- **Designed a Reward System**: Encouraging the AI to reduce its distance to waypoints and complete the course efficiently.
- **Trained the AI**: Leveraging Proximal Policy Optimization (PPO) to teach the agent how to navigate and adjust to wind conditions.

### Step 3: Human-AI Showdown
Once the AI was trained, I added a **racing mode** where players could compete against the AI in real-time. This involved:

- **Adding a Second Boat**: The player-controlled boat had its own state and controls, independent of the AI.
- **Rendering Both Boats**: Using Pygame to visualize the race and display wind indicators, waypoint markers, and boat positions.
- **Race Logic**: Comparing finish times or progress if the time limit expired.

---

## Key Challenges and Solutions

### Balancing Realism and Playability
Sailing simulations can become overly complex. I simplified the physics enough to ensure the game was intuitive but still required skill and strategy. For example, instead of modeling every aspect of sail aerodynamics, I used a simplified polar diagram to calculate boat speed based on wind angle.

<div style="text-align: center;">
  <img src="http://kodendaal.github.io/assets/polarplot.png" style="width: 400px; height: auto;">
</div>


### Shaping the AI’s Learning (WIP)
Early training results showed the AI struggling to stay on course. Adjustments to the reward function—such as incremental rewards for reducing distance to waypoints—helped the AI improve. Randomizing wind directions and starting positions during training made the AI more robust.

### Integrating the Human Experience (WIP) 
Adding a human-playable mode meant balancing the controls for accessibility and precision. It was important to give players tools like wind direction indicators and clear feedback on sail trim efficiency.

---

## What Makes It Fun? (WIP)

1. **Dynamic Wind Mechanics**: Players must constantly adjust their strategy based on wind direction and strength.
2. **Challenging AI**: Competing against an AI that learns and adapts offers a unique and unpredictable challenge.
3. **Race Variety**: Multiple waypoint courses and randomized conditions ensure no two races are the same.

---

## Lessons Learned

### Iteration is Key
Game development is an iterative process. From tweaking boat physics to refining the reward function for the AI, each improvement brought the game closer to its vision.

### The Joy of Visual Debugging
Watching the AI’s behavior evolve through Pygame rendering was both enlightening and entertaining. It helped me identify issues and celebrate milestones as the agent learned to sail efficiently.

### Collaboration Enhances Creativity
Leveraging open-source tools like Stable Baselines3 and Pygame made the project manageable and fun. The community’s resources and support were invaluable.

---

## What’s Next?
The journey doesn’t end here. Future plans include:

- **Multiplayer Mode**: Allowing players to race against each other online.
- **Advanced AI**: Training agents with more complex physics and weather conditions.
- **Customizable Boats**: Giving players the ability to design and upgrade their vessels.

---

## Conclusion

Building this sailing regatta game has been an incredible adventure. It’s a blend of programming, physics, and game design that’s as challenging as it is rewarding. Whether you’re setting out to build your own game or just curious about how games like this come together, I hope this story inspires you to hoist your own sails and start your journey.

The full code for this project is available on my GitHub repository. Feel free to explore and contribute!

Happy sailing!


