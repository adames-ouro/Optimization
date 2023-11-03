# Optimization - Traveling Salesman Problem 

---

## Problem Statement:
In the Traveling Salesman Problem (TSP), we have a set of cities, and the distances between each pair of cities are known. The problem is to find the shortest possible route that visits each city exactly once and returns to the starting city (often referred to as the depot).

---
### Formulas used:

- **Number of cities to visit (0 represents the depot)**: 
    ![N Formula](https://latex.codecogs.com/svg.latex?\color{white}N)

- **Set of cities**:
    ![I Formula](https://latex.codecogs.com/svg.latex?\color{white}I%20=%20\{0,...,N\})

- **Set of cities excluding depot**:
    ![K Formula](https://latex.codecogs.com/svg.latex?\color{white}K%20=%20\{1,...,N\})

- **Each city i visited in order excluding depot**:
    ![v_i Formula](https://latex.codecogs.com/svg.latex?\color{white}v_{i})

- **Distance between city i to city j**:
    ![d_ij Formula](https://latex.codecogs.com/svg.latex?\color{white}d_{ij})

- **Binary decision variable for city transition**:
    ![X_ij Formula](https://latex.codecogs.com/svg.latex?\color{white}X_{ij}%20=%201%20\text{if%20city%20j%20is%20visited%20from%20city%20i})

- **Objective function for TSP**:
    ![Objective function](https://latex.codecogs.com/svg.latex?\color{white}Z%20=%20\sum_{i=0}^{n}%20\sum_{j=0}^{n}%20d_{ij}%20*%20X_{ij})

- **Reach every city from exactly one predecessor**:
    ![Constraint 1](https://latex.codecogs.com/svg.latex?\color{white}\sum_{i=0}^{n}%20X_{ij}%20=%201%20\forall%20j%20\in%20I)

- **Leave every city to exactly one successor**:
    ![Constraint 2](https://latex.codecogs.com/svg.latex?\color{white}\sum_{j=0}^{n}%20X_{ij}%20=%201%20\forall%20i%20\in%20I)

- **Subtour elimination**:
    ![Constraint 3](https://latex.codecogs.com/svg.latex?\color{white}(N%20-%201)(1%20-%20X_{ij})%20\geq%20v_{i}%20-%20v_{j}%20+%201%20\forall%20i,%20j%20\in%20K)

- **Variable types for X and v**:
    ![Variable type 1](https://latex.codecogs.com/svg.latex?\color{white}X_{ij}%20\in%20\{0,1\})
    ![Variable type 2](https://latex.codecogs.com/svg.latex?\color{white}v_{i}%20\in%20\{0,...,N-1\})


---

## Q-learning in Reinforcement Learning for TSP

### Introduction

Q-learning is a model-free reinforcement learning algorithm used to find the optimal action-selection policy for a given finite Markov decision process. In simpler terms, it's an algorithm that helps an agent (like a robot or drone) learn how to choose optimal actions that yield the most reward over time.

### Q-function

The central component of the Q-learning algorithm is the Q-function. It's denoted as $Q(s, a)$ and represents the expected reward of taking action $a$ in state $s$.

The Q-function is updated using the Bellman equation:

\begin{equation}
Q(s, a) = r + \gamma \max_{a'} Q(s', a')
\end{equation}

Where:

- $r$ is the reward received after taking action $a$ in state $s$.
- $\gamma$ is the discount factor, which models the agent's consideration for future rewards. A high value (close to 1) makes the agent prioritize long-term reward over short-term reward.
- $s'$ is the next state.
- $a'$ is any possible action in state $s'$.


## Algorithm

1. Initialize Q-values arbitrarily for all state-action pairs.
2. For each episode:
    1. Start at a random state.
    2. For each step in the episode:
        1. Choose an action $a$ from state $s$ using a policy derived from the current Q (e.g., $\epsilon - greedy$).
        2. Take the action, and observe the reward $r$ and the new state $s'$.
        3. Update the Q-value using the Bellman equation.
        4. Set $s = s'$.
    3. Repeat until a terminal state is reached.

## Exploration vs. Exploitation

A significant challenge in Q-learning is the trade-off between exploration (trying new actions) and exploitation (relying on known information). A common solution is the $\epsilon - greedy$ policy:

- With probability $\epsilon$, choose a random action.
- With probability $1 - \epsilon$, choose the action with the highest Q-value.

Over time, $\epsilon$ is decreased so that the agent explores less and exploits more.

---

## Simulated Annealing for the Traveling Salesman Problem (TSP)

### Introduction

Simulated Annealing (SA) is a probabilistic optimization technique inspired by the annealing process in metallurgy. Annealing involves heating a material and then cooling it slowly. Simulated annealing applies this concept to find an approximation to the global optimum of a function.

The Traveling Salesman Problem (TSP) is a classic optimization problem where a salesman wishes to visit a number of cities exactly once and return to the starting city while minimizing the total distance traveled.

### The Simulated Annealing Algorithm for TSP

1. **Initialization**:
    - Start with an initial feasible solution (usually a random permutation of cities).
    - Set an initial temperature $T$ and a minimum temperature $T_{\text{min}}$.
    - Choose a cooling rate $\alpha$ (typically between 0.8 and 0.99).

2. **Iterative Process**:
    - While $T > T_{\text{min}}$:
        - For a number of iterations:
            - Generate a neighbor solution by making a small change to the current solution (e.g., swapping two randomly selected cities).
            - Calculate the difference in the cost (distance) between the new solution and the current solution: $\Delta E$.
            - If the new solution is better or if a random number between 0 and 1 is less than $e^{-\Delta E/T}$, accept the new solution as the current solution.
        - Decrease the temperature: $T = \alpha \times T$.

3. **Termination**:
    - When the temperature is less than $T_{\text{min}}$, the algorithm terminates, and the best-found solution is returned.

### Key Concepts:
- **Temperature $T$**: It's a control parameter that determines the probability of accepting a worse solution than the current one. A high temperature increases the chance of accepting worse solutions, promoting exploration, while a low temperature tends to accept only better solutions, promoting exploitation.

- **Cooling Schedule**: How the temperature decreases over time. A typical method is geometric cooling, where the temperature is multiplied by a constant factor $\alpha$.

- **Neighbor Solution Generation**: In TSP, a neighbor can be generated by various methods such as swapping two cities, reversing a subsection of the tour, or other perturbations.

