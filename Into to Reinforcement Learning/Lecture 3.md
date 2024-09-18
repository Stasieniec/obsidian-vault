# Markov Decision Process (MDP)

An MDP is defined by a 5-tuple ($S, A, P, R, \gamma$)
- $S$: Set of states
- $A$: Set of actions
- $P$: Transition probability, $P(s'|s, a)$, which defines the probability of reaching state $s'$ from state $s$ by taking action $a$.
- $R$: Reward function, $R(s, a)$, the immediate reward received after transitioning from state $s$ via action $a$
- $\gamma$: Discount factor, which weighs future rewards (typically $0<\gamma < 1)$. The close $\gamma$ is to $1$, the more future rewards are valued

Goal - find optimal policy $\pi$, which maps states to actions, maximizing the expected cumulative reward. (maximizing the value function, which represents the expected return from any given state)

# Value Function and Bellman Equation

**Value function** $V^\pi (s)$ for a policy $\pi$ is the expected cumulative reward starting from state $s$, following policy $\pi$. The **Bellman equation** describes the recursive nature of this function:
$$V^\pi (s) = R(s) + \gamma \sum_{s'} P(s'|s, \pi(s)) V^\pi (s')$$
# Optimal Value Function and Policy

The **optimal value function $V^*(s)$** gives the maximum expected reward from any state s across all possible policies. The bellman equation for the optimal value function is:
$$V^* (s) = \arg\max_{a}[R(s) + \gamma \sum_{s'} P(s'|s, a) V^*(s')]$$
From this, the **optimal policy** $\pi^*$ can be derived by choosing the action $a$ that maximizes the right-hand side of the equation\

# Value Iteration

This algorithm is used to find the optimal value function and, eventually, the optimal policy.

1. Initialization: Set $V(s) = 0$ for all states
2. Update: Repeatedly update the value function using the Bellman optimality equation: $$V(s) \leftarrow R(s) + \gamma \max_a \sum_{s'} P(s'|s, a) V(s') $$
3. Convergence: Repeat the update step until $V(s)$ converges.

The value iteration does not explicitly compute a policy, but indirectly arrives at the optimal one by improving the value estimates

# Policy Iteration

Another approach for solving MDPs:
1. Policy evaluation: Given a policy $\pi$, evaluate its value function $V^\pi(s)$ using the Bellman equation
2. Policy Improvement: Update the policy by selecting actions that maximize the expected return: $$\pi'(s) = \arg \max_a \sum_{s'} P(s' | s, a) V^\pi (s')$$
The process alternates between policy evaluation and improvement until convergence

# Comparison: Value Iteration vs. Policy Iteration

- Value Iteration: More efficient for large state/action spaces since it avoids evaluating policies explicitly, updating value functions directly
- Policy Iteration: Typically converges faster for small problems but involves the costly evaluation of policies
# Model-based Reinforcement Learning

When the environment's transition probabilities and rewards are unknown, the agent can learn an approximate model from experience (episodes of state transitions):
1. Lean transition probabilities $P(s'|s, a)$ from experience
2. Learn reward function $R(s)$, averaging rewards over episodes
