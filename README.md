# Optimization - Traveling Salesman Problem 

---

## Problem Statement:
In the Traveling Salesman Problem (TSP), we have a set of cities, and the distances between each pair of cities are known. The problem is to find the shortest possible route that visits each city exactly once and returns to the starting city (often referred to as the depot).

---
### TSP formulation: 

N = # number of cities to visit ( 0 represents depot )

I = set of cities = {0,...,N}

K = set of cities excluding depot = {1,...,N}

$v_{i} = $ each city i visited in order excluding depot.

$d_{ij} = $ distance between city i to city j.

$X_{ij} $ $ = 1 $ if city j is visited from city i.

MIN $ Z = \sum_{i=0}^n \sum_{j=0}^n {d_{ij} * X_{ij}}$

subject to:
    
1)  reach every city from exactly one predecessor

    $\sum_{i=0}^n {X_{ij}} = 1 $ $\forall j$ $\in$ I

2)  leave every city to exactly one succesor

    $\sum_{j=0}^n {X_{ij}} = 1 $ $\forall i$ $\in$ I

3) subtour elimination

    $ (N - 1)*(1 - X_{ij}) $ $ \geq $ $ v_{i}  - v_{j} + 1  $   $\forall i, j$ $\in$ K

4) variable types: x as binary, v as integer

    $ X_{ij} $ $\in$ {0,1} ,  $ v_{i} $ $\in$ { 0, ... , N - 1 }
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

