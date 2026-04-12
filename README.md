# MountainCar-v0: Continuous Control via Linear Function Approximation

This repository contains the implementation of **Semi-Gradient SARSA** with **Tile Coding** to solve the `MountainCar-v0` environment. This project marks the transition from tabular reinforcement learning to function approximation, enabling an agent to operate in a continuous state space.

## Environment Overview
In the Mountain Car problem, an underpowered car is stuck in a valley. The goal is to reach the flag atop the right hill (position > 0.5). 
* **State Space:** Continuous $[\text{position}, \text{velocity}]$ representing the car's physical state.
* **Challenge:** The car cannot drive straight up the hill; it must learn to build momentum by rocking back and forth.
* **Reward:** $-1.0$ for each time step, incentivizing the agent to find the fastest path to the goal.

## Technical Implementation

### 1. Tile Coding (Feature Engineering)
Because the state space is continuous, a tabular approach is impossible. We implemented a **Tile Coder** to discretize the space into overlapping grids:
* **Tilings:** 8 overlapping layers to provide fine resolution.
* **Tiles per Dimension:** 8x8 per tiling, resulting in a total of 512 binary features.
* **Generalization:** Overlapping tiles allow the agent to generalize learning from one state to similar neighboring states, significantly improving sample efficiency.

### 2. Semi-Gradient SARSA
We utilized a linear function approximation where the Q-value is the dot product of a weight vector $\mathbf{w}$ and the feature vector $\mathbf{x}(s)$:
$$Q(s, a, \mathbf{w}) = \mathbf{w}_a^T \mathbf{x}(s)$$

* **On-Policy Learning:** The agent updates its weights based on the actions it actually takes, ensuring stability.
* **Weight Updates:** We use a step-size $\alpha$ normalized by the number of tilings ($\alpha/n$) to prevent weight divergence.

## Results and Analysis

### Learned Value Function (`The Heatmap.png`)
The heatmap visualizes the **Cost-to-Go** (the estimated steps to reach the goal).

![Value Function Heatmap](The%20Heatmap.png)

* **Interpretation:** The yellow peak indicates the "bottom" of the valley where the agent is furthest (in terms of steps/cost) from the goal.
* **Convergence:** As training progresses, the cost-to-go near the goal (position 0.5) correctly drops toward zero.

### Learned Policy (`The Quiver Plot.png`)
The quiver plot illustrates the directional strategy learned by the agent.

![Policy Quiver Plot](The%20Quiver%20Plot.png)

* **Strategy:** The agent successfully learns to push left when moving left to gain height on the rear slope, then pushes right to utilize gravity and momentum to reach the flag.
