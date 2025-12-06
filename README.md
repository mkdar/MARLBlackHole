# MARLBlackHole

This repository contains a Jupyter Notebook implementing a multi-agent reinforcement learning (MARL) environment where agents attempt to survive and maintain orbits around a simulated black hole. The project includes both Newtonian-gravity and circular-orbit modes, reward shaping, curriculum learning, and a full PPO training pipeline.

## Contents

The notebook includes the complete codebase, organized into the following components:

### Drone and Mothership Classes

* Defines agent state (position, velocity, fuel, anti-gravity).
* Implements thrusting, movement, resource usage, and survival checks.

### MARLBlackHole Environment

* Simulates black hole physics: gravity, event horizon, ISCO (innermost stable circular orbit), orbital instability, and plunge acceleration.
* Supports multiple agents (one mothership and several drones).
* Includes resource nodes for harvesting fuel and anti-gravity.
* Handles observations, step logic, death conditions, and multi-agent interactions.

### Reward Functions

Two reward models are provided:

* Newtonian orbit reward
* Circular-orbit reward

These encourage inward exploration, orbital stability, tangential motion, resource conservation, and avoidance of the event horizon.

### Curriculum Wrapper

* Gradually increases training difficulty in stages.
* Controls satellite initialization at reset.
* Adds light shaping rewards in early stages to speed up PPO learning.
* Moves through stages automatically based on episode count.

### Shared PPO Implementation

* Shared actor-critic network for all agents.
* PPO clipping objective.
* GAE-Lambda advantage estimation.
* Reward normalization.
* Training statistics tracking (policy loss, value loss, entropy, KL).

### PPO Training Loop

* Runs multi-agent PPO training for several epochs.
* Logs episode returns and losses.
* Stores training history for plotting.

### Plotting and Visualization

* Returns, losses, entropy, and KL curves.
* Optional rendering of trajectories or GIFs of trained behavior.

## Purpose

This project serves as a complete, self-contained MARL experiment:

* Orbit stabilization under unstable physics
* Multi-agent coordination and survival
* Curriculum learning in difficult reinforcement learning tasks
* Reward shaping for sparse and unstable environments

## Usage

Open the notebook in Jupyter and run the cells top-to-bottom.
Training begins with a call such as:

```python
ppo_agent, env, history = train_shared_ppo(
    epochs=500,
    steps_per_epoch=4000,
    n_satellites=6,
    orbit_mode="newtonian",
    seed=42
)
```

This produces a trained PPO agent and logs results for analysis.
