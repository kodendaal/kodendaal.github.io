# Racing the Wind: Building a Python-Powered Sailing Regatta Simulator ⛵️💨

Ever wondered what it feels like to jibe around the leeward mark with three hungry competitors nipping at your transom, all without getting your deck shoes wet? I did. So I wrote a little game that drops you into a tactical regatta against a fleet of AI skippers, each with their own quirks and weaknesses.

Under the hood, it’s a mash-up of real-world sailing physics, control theory, and a sprinkle of video-game sparkle. In this post, I’ll unpack how it all works—from weather-helm math to multi-boat race orchestration—and share a few “gotchas” I hit along the way.

---

## 1. A Quick Tacking Tour 🚤➡️🚤

Before we dive deep, here’s the ship's log:

*   **Language & Libraries:** Pure Python 3.12 and Pygame for the real-time graphics and control loop.
*   **Play Modes:**
    1.  **Single-Rudder (Arcade):** Simple, intuitive control. Just point the boat where you want to go.
    2.  **Dual-Control (Simulation):** Manage both the rudder and the mainsheet. Nail the trim for max speed, or stall your sails and watch the fleet pass you by.
*   **Opponents:** A gallery of pluggable AI strategies—from a "Happy-Camper" rookie who over-steers to a terrifyingly precise PID-driven hotshot.
*   **Why “Regatta”—Not Just a “Racing Game”?:** Because raw speed isn't enough. Winning depends on tactics: playing the wind shifts, choosing the perfect layline, and executing flawless mark roundings.

Spin it up (`python -m game.start_menu`), and you’ll find yourself on a virtual start line with live wind arrows swirling overhead. Hold your course, trim those sails, and let's see who rounds the top mark first!

---

## 2. Zooming Out: The Architecture at Hull Speed

A good boat is balanced, and so is good code. The simulator is built on a loosely-coupled, swappable design inspired by the Strategy Pattern.

```
         +-------------------+
         |   Environment     |  ← Simulates gusts, shifts, and lulls
         +-------------------+
                  ▲
                  │ wind_vector
+--------+   updates   +---------------------+
|  Boat  |────────────▶|    RaceSimulator    |  ← Manages laps, marks, timing
+--------+             +---------------------+
   ▲   ▲                      ▲
   │   │ strategy decides      │ draws all objects
   │   └─────┐          +--------------+
   │         └──────────|  SimDrawer   |  ← Pygame rendering engine
   │ control commands   +--------------+
   │
+------------------+
| Strategy (AI)    |  ← Pluggable brains (PID, Manual, etc.)
+------------------+
```

Each component has one job:
*   The **`Environment`** is the weather god, creating wind for the fleet.
*   The **`RaceSimulator`** is the race committee—it sets the course, starts the race, and times the laps.
*   Each **`Boat`** instance is a self-contained physics object.
*   A **`Strategy`** is the brain of a skipper, deciding what commands to send to its `Boat`.
*   The **`SimDrawer`** puts it all on the screen.

This modularity is key. You can swap a `Boat` subclass to experiment with a catamaran, plug in a new `Strategy` to test your AI, or even hot-load a fresh `Environment` to simulate a sudden squall.

---

## 3. Getting Physical: From Wind Angles to Wake

This isn't just `boat.x += 5`. The physics model blends real sailing principles with a few performance-friendly simplifications.

### 3.1 Polar Performance and Apparent Wind

In the real world, a boat's potential speed is dictated by its **polar diagram**—a chart that maps its speed for a given wind speed and angle. I baked these performance curves into `polar.py`, which interpolates the data to find the boat's target speed.

```python
# Get the boat's theoretical top speed for the conditions
target_speed = polar.get_speed(true_wind_angle, true_wind_speed)
```

But here's the sailor's secret: a moving boat creates its own wind! The wind you *feel* on board—the **apparent wind**—is a vector sum of the true wind and the wind from your own motion. This apparent wind is what actually drives the sails. The physics loop constantly recalculates it to determine the drive and drag forces.

```python
# Simplified force balance, run every tick (60 Hz)
F_drive  = C_drive * apparent_wind_speed**2 * sail_efficiency * cos(heel_angle)
F_lateral = ... # The sideways force from the keel
F_drag   = C_drag * boat_velocity**2

# Euler integration to update velocity and position
acceleration = (F_drive - F_drag) / boat_mass
boat_velocity += acceleration * dt
```

### 3.2 Weather Helm & Heeling

To make the boats feel alive, I added two crucial effects:

1.  **Heeling:** As wind pressure builds, the boat leans (heels) over. This is not just for looks! The `cos(heel_angle)` term in the physics equation means a heavily heeled boat is less efficient—it's "spilling" wind and power. This encourages the player (or AI) to trim correctly.
2.  **Weather Helm:** Wind pressure on the sails tries to push the boat's bow up into the wind. A real sailor feels this as constant pressure on the tiller. In the code, this is a small force that the rudder must constantly fight, making steering a more dynamic challenge.

```python
# From src/boat.py - a constant force the rudder must overcome
WEATHER_HELM_FORCE = 0.02
```

---

## 4. Bot Brains: The Strategy Pattern in Action 🧠

Every AI skipper is a Python class in the `strategies/` directory, implementing a simple interface:

```python
class Base:
    def update(self, boat_state, environment_state):
        """
        Analyzes the situation and returns control commands.
        e.g., return rudder_angle, sail_trim_angle
        """
        raise NotImplementedError()
```

This makes it trivial to add new competitors:

*   **Default Tactician:** A solid all-rounder. It aims for the next mark but knows when to tack or jibe if it's sailing at a poor angle. Surprisingly hard to beat for beginners.

*   **PID-Powered Pro:** This skipper uses two Proportional-Integral-Derivative (PID) controllers—one for the rudder to hold a precise course, and another for the sail to maximize efficiency. It's smooth, ruthlessly efficient, and a true test of skill. Tweaking its `Kp`, `Ki`, and `Kd` gains for different wind strengths is a fascinating exercise in control theory.

*   **"Happy-Camper" Rookie:** My personal favorite for an ego boost. It's programmed to over-steer into turns and often forgets to ease the sails when turning downwind, causing it to slow down dramatically.

> **DIY Challenge:** Drop a file in `strategies/`, implement the `update` method, and your very own bot will be on the start line for the next race!

---

## 5. The Race Director: Orchestrating the Chaos

The `RaceSimulator` is the unsung hero. It's the central coordinator that:

1.  **Sets the Course:** Places the starting line and rounding marks.
2.  **Manages the Start:** Runs the 5-minute countdown sequence using `time.perf_counter()` for precision. Crossing the line early is a penalty!
3.  **Runs the Main Loop:** At 60 FPS, it tells the `Environment` to update the wind, asks each `Strategy` for its move, applies that move to the `Boat`, and checks for rule infringements.
4.  **Calls the Finish:** It logs lap splits and final race times to a CSV, so you can analyze your performance (or your AI's) after the race.

To keep things snappy even with a full fleet, the physics updates run in a worker thread, separate from the main Pygame rendering loop. This ensures a smooth 60 FPS, even on a Raspberry Pi.

---

## 6. Pretty Pictures: Visuals That Teach Sailing

The UI isn't just chrome; every element provides critical feedback that subconsciously teaches sailing heuristics.

*   ⛵ **Sail Efficiency Glow:** The sail itself changes color: **green** for optimal trim (±5°), **amber** if it's starting to luff (too tight), and **red** if it's fully stalled (too loose). Players quickly learn to keep it green.
*   💨 **Wind Arrows:** Animated arrows show the *true* wind direction and strength, helping you spot shifts and puffs across the course.
*   📏 **Laylines:** Dotted lines project from the next mark, showing the optimal tacking angles. When the wind shifts, the laylines move—instantly telling you if you've been "lifted" or "headed."

Without realizing it, players start to internalize real sailing tactics: *head up in a lift, bear away in a header!*

---

## 7. Performance Tricks (a.k.a. Hitting 60 FPS)

Keeping a real-time physics simulation smooth requires a few tricks:

1.  **Blit Once, Rotate Often:** The boat sprite is loaded once. Each frame, we use the hardware-accelerated `pygame.transform.rotozoom` to rotate it. This is much faster than rotating the source image.
2.  **Dirty-Rect Redrawing:** Instead of redrawing the whole screen every frame, we only update the rectangular areas ("rects") where things have moved—the boats, marks, and UI text.
3.  **Vectorized Math:** In hot paths like the polar diagram lookup, I use NumPy to perform vectorized calculations, which is significantly faster for numerical operations than pure Python loops.

The result? The simulation hums along at under 2ms per boat per frame on my old Surface Laptop.

---

## 8. Next on the Horizon 🌅

The logbook is always open for new ideas. Here’s what I’m charting next:

*   **Currents & Tides:** Integrating real-world GRIB files to simulate tidal currents, adding another layer of coastal strategy.
*   **Post-Race Telemetry:** Building a tool to play back race data and visualize key metrics like VMG (Velocity Made Good) and time lost in tacks.
*   **Reinforcement Learning Skipper:** Training a neural network where the reward is a faster finish time and the actions are continuous rudder and sail commands. Can a machine out-sail a human tactician?

---

*Got questions, feature ideas, or salty feedback? Let’s chat in the GitHub issues—or hoist a beer and tell me what I broke.*
