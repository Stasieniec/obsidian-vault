# Model-Free Reinforcement Learning

When we don't have the model of how states transitions work or how rewards are distributed, we can estimate this from experience, without building a full Markov Decision Process model.

In model-free prediction, we aim to estimate the expected return (value function) of a given policy without access to the transition probabilities or rewards of the environment.

Two main methods:
- Monte Carlo (MC) methods
- Temporal Difference (TD) learning

# Monte Carlo Methods

## 1. Monte Carlo Value Estimation

Monte Carlo - repeated random sampling to estimate the value function.
RL - learn from complete episodes (sequences of state-action-reward transitions that eventually reach a terminal state)

For a policy $\pi$, the value function of a state $s$ is the expected cumulative reward when starting in state $s$ and following $\pi$. This is written as: $$ V^\pi (s) = E [R(s_0) + \gamma +  R(s_1) +\gamma^2 R(s_2) + ... | s_0 = s]$$
Monte Carlo methods estimate this by:
1. Sampling N episodes from the policy $\pi$ and recording the total reward for each episode
2. Averaging the cumulative reward over those episodes to estimate the value of each state

**Example:** While playing a game, simulating 5 episodes starting from state $s_0$, we got the following rewards: 1, 2, 3, 4, 5. The Monte Carlo estimate for the value of $s_0$ is the average: $$V^\pi (s_0) \approx \frac{1 + 2 + 3 + 4 + 5}{5} = 3$$
## 2. Monte Carlo Method Advantages
- Model-free: No need to know the transition probabilities or rewards beforehand
- Easy to implement: Monte Carlo methods rely on averaging observed outcomes
## 3. Monte Carlo Limitations
Monte Carlo methods can only be applied to episodic tasks ( tasks where the episodes terminate)
High variance: Since they rely on complete episodes, the estimate can be noisy
They are inefficient for non-terminating or continuous tasks


# Temporal Difference (TD) Learning

TD is another approach to estimate the value of a policy. It learns from incomplete episodes and updates value estimates incrementally, making it suitable for environments where episodes do not end, or where we want to update the value after each step.
## 1. TD Update Rule
Instead of waiting for an episode to finish, TD methods update the value estimate of a state $s$ after observing just one transition from $s$ to $s'$, receiving a reward $R$. The update rule is: $$V(s_t) \leftarrow V(s_t) + \alpha(R_{t+t} + \gamma V(S_{t+1}) - V(s_t))$$
The value of $s_t$ should get closer tio the immediate reward $R_{t+1} plus the discounted estimate of the next state $V(s_{t+t})$.

## 2. Advantages of TD Learning
- More efficient: TD methods update the value after each step, allowing for faster convergence
- Works with non-episodic tasks: Since TD updates after each transition, it doesn't need the episodes to terminate
## 3. Disadvantages of TD learning
TD methods introduce **bias** because they use estimates rather than actual observed returns

# Monte Carlo vs. Temporal Difference (TD)


| **Aspect**                  | **Monte Carlo (MC)**                                 | **Temporal Difference (TD)**                    |
| --------------------------- | ---------------------------------------------------- | ----------------------------------------------- |
| Learning from           | Complete episodes                                    | Each step (before the episode ends)             |
| Environment Type        | Episodic (finite-length)                             | Both episodic and continuous                    |
| Update rule             | Based on the average cumulative reward over episodes | Based on the reward and value of the next state |
| Variance/Bias trade-off | High variance, no bias                               | Low variance, biased                            |
| Efficiency              | Less efficient (must wait for episodes to finish)    | More efficient (updates at every step)          |

# Incremental Monte Carlo and TD Updates
Both MC and TD methods can be implemented incrementally:
- Incremental MC: Updates the value of a state based on the average return over multiple episodes $$V(st​)←V(st​)+N(st​)1​(Gt​−V(st​))$$
- Incremental TD: Updates the value after every time step based on the reward and the value of the next state $$V(st​)←V(st​)+α(Rt+1​+γV(st+1​)−V(st​))$$


# Conclusion
- Monte Carlo - intuitive, useful for episodic tasks. Suffer from high variance and inefficiency in non-terminating environments
- TD - more efficient learning, especially in continuous tasks, but at the cost of introducing bias.

In practice, TD methods are more commonly used.