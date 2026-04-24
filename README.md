# Lab 5: Function Approximation with Semi-Gradient SARSA
**MSDS 684: Reinforcement Learning | Regis University**

## Project Overview
This project solves the `MountainCar-v0` environment, which features a continuous state space (Position and Velocity). To handle the infinite state space, we transition from tabular Q-learning to **Linear Function Approximation** using a custom-built **Tile Coding** constructor.

## Technical Methodology
### Tile Coding (From Scratch)
We implemented a feature constructor that discretizes the 2D observation space into **8 overlapping tilings** with **8x8 tiles** each. This "coarse coding" allows the agent to generalize learning across neighboring states, which is essential for mastering the momentum-based physics of the mountain car.

### Semi-Gradient SARSA
We utilize an on-policy control method where the weight vector $\mathbf{w}$ is updated using the semi-gradient rule:
$$\mathbf{w}_{t+1} \leftarrow \mathbf{w}_t + \alpha [R_{t+1} + \gamma \hat{q}(S_{t+1}, A_{t+1}, \mathbf{w}_t) - \hat{q}(S_t, A_t, \mathbf{w}_t)] \nabla \hat{q}(S_t, A_t, \mathbf{w}_t)$$

## Experimental Results
The agent successfully learned to "rock" the car back and forth to gain enough potential energy to reach the goal. Our analysis includes four core visualizations:

| Value Function Heatmap | Policy Action Map |
| :---: | :---: |
| ![Value Function](Learned%20Value%20.png) | ![Policy Map](policy%20visualization.png) |

| Convergence Comparison | State-Space Trajectory |
| :---: | :---: |
| ![Convergence](convergence%20comparison.png) | ![Trajectory](simple%20trajectory.png) |

## Repository Structure
- `Week5_FunctionApproximation_ValueMethods.ipynb`: Full implementation of Tile Coding and SARSA.
- `Kakshapati_Barsha_Lab_5_Report.pdf`: APA-formatted formal lab report.
- `requirements.txt`: Python environment dependencies.

## References
Sutton, R. S., & Barto, A. G. (2018). *Reinforcement Learning: An Introduction*. MIT Press.
