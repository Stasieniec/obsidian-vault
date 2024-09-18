# Reinforcement Learning (recap)
- State: A complete representation of the environment at a given time
- Action: The possible moves the agent can take from a given state
- Reward: A scalar feedback signal that tells the agent how well it is performing.
Goal: maximize the cumulative reward over time by learning the best actions to take in each state

# Model-Free Reinforcement Learning

In model-free RL, the agent does not have a model of the environment. Instead of predicting the future states or rewards, it learns directly from experiences through trial and error.
### From knowing What's Good to How to Act
How to derive optimal actions?
- Value function $V(s)$: This tells us how good a particular state $s$ is, based on the expected reward from that state.
- Action-Value Function $Q(s, a)$: This tells us how good it is to take action $a$ in state $s$.

# Q-Learning

Q-learning - model-free control algorithm that aims to learn the optimal action-value function $Q^*(s, a)$, which gives the best action to take from any state.

### Temporal Difference (TD) Learning

Temporal Difference learning is a method used by the algorithm of Q-Learning. The agent updates its estimates of $Q$ values based on observed transitions. 
Idea: adjust the estimate of $Q(s, a) based on how much better or worse the actual reward and next state's value are compared to the previous estimate.

The update rule for Q-learning is:$$Q(s, a) \leftarrow Q(s, a) + \alpha [r + \gamma \max_{a'}Q(s', a') - Q(s, a)]$$
Where:
- $s$, $a$ are the current state and action
- $r$ is the reward received after taking action $a$
- $s'$ is the next state after taking action $a$
- $a'$ is the action in the next state $s'$ that maximizes $Q$
- $\alpha$ is the learning rate, determining how much new information overrides old.
- $\gamma$ is the discount factor, determining how much future rewards are valued compared to immediate rewards.
### Exploration vs. Exploitation
Q-learning often uses an $\epsilon$-greedy policy for action selection, which balances exploration (trying out new actions) and exploitation (choosing the best-known action based on the learned Q-values). With probability $\epsilon$, the agent explores, and with probability $1-\epsilon$, the agent exploits.

# Tabular Q-Learning

When the state and actions spaces are small, Q-learning can be implemented using a table where each entry corresponds to a $Q(s, a)$ value. This is the tabular Q-learning method. In larger environments, tables become impractical, and function approximations like neural networks are used instead (this is the basis of Deep Q-Networks, DQNs).

The tabular Q-learning algorithm can be summarized in the following steps:
1. Initialize $Q(s, a)$ arbitrarily (usually to 0)
2. For each episode
	1. Start from an initial state $s_0$
	2. Choose an action $a$ using $\epsilon$-greedy
	3. Take action $a$, observe the reward $r$ and the next state $s'$
	4. Update the Q-value: $$Q(s, a) \leftarrow Q(s, a) + \alpha [r + \gamma \max_{a'}Q(s', a') - Q(s, a)]$$
	5. Repeat the process until the episode ends

# Temporal Difference (TD) Target

TD target - expected return from the current state-action pair, which is used to update the Q-value:$$\text{TD Target} = r + \gamma \max_{a'}Q(a', a')$$
The TD error is the difference between the current Q-value and the TD target: $$δ=r+γ \max_{a'}​Q(s′,a′)−Q(s,a)$$
This error drives the learning process, adjusting the Q-values toward more accurate estimates.

# Convergence

Q-learning converges to the optimal action-value function $Q^*(s, a)$ under certain conditions, such as proper exploration and decresing learning rates

# Model-Free vs. Model-Based RL

- Model-based: The agent learns or knows the model of the environment and uses this to plan its actions
- Model-free: directly learns the optimal policy or value function from interactions without learning the transition dynamics.