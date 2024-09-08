# Markow Decision Processes

### General RL
Agent tries to maximize the total amount of reward while interacting with the environment

### RL vs SL
- Sequential data as input
- The learner is not told which actions to take, but must discover which actions yield the most reward by trying them
- Trial-and-error exploration (exploration vs exploitation)
- There is no supervisor, only a reward signal, which is also delayed
### RL agent might include one or more of the following
- Policy: agent's behavior function
- Value function: how good is each state and/or action
- Model: agent's representation of the environment

Content:
1. Markov Process
2. Markow reward process
3. Markov decision process


# Markov process
## Markov property
- The future is independent of the past given the present
- A state s is Markov if it is determined by the previous state, not all previous states
- The state captures all relevant information from the history
- Once the state is known, the history may be thrown away
- The state is a sufficient statistic of the future

## State transition matrix
- For a Markov state s and successor state s prime, the state transition probability is defined by : $$ P_{ss'} = P(S_{})$$\
- State transition matrix P defines transition probabilities from all states s to all successor states s prime
## Markov process (chain)
Memoryless random process: sequence of random states with the Markov property
# Markov reward process

### Bellman equation for MRP
The value function can be decomposed into two parts:
- Immediate reward of the next state
- Discounted value of successor state $$\gamma v(S_{t+1})$$
## Value function
- he state-value function of an MDP is th eexpected return starting from state s, and then following policy pi
- The action-value function is the expected