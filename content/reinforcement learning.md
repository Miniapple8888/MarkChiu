recall: 3 types of machine learning
1. supervised learning -> given labels
2. unsupervised learning -> no label
3. reinforcement learning -> in between (has numeric feedback: rewards & punishments)

modeled as a [[markov decision processes]]:
- single agent given states $S$ and possible actions $A$
- each timestep, observe state + reward -> do action
	- assume full observability
- no given transition model and no given reward model
	- model-free, must discover new states and rewards
- goal: maximize discounted reward over time
	- find optimal policy

RL is hard:
- reward is infrequent
	- difficult to determine which action cause reward/lead to win/loss
- action long term utility

## tradeoff explore or exploit
- **explore**: better for long term, learn more about different states and actions
- **exploit**: better short term to make gains (maximize reward value)
- $\epsilon$-greedy strategy: 
	- $\epsilon=0$ never explore, always exploit
	- $\epsilon=1$ always explore, never exploit 

## q-learning
build a q table of states x actions
value-based method (reward)

- episodes: start and finish of sequence of states from $s_0$ to $s_{terminal}$ 
- steps: each state taken
	- pick action
	- observe next state, reward
	- compute reward

$$Q(s_t,a_t)=Q(s_t,a_t)+\alpha(r_{t+1}+\gamma \max_a Q(s_{t+1},a)-Q(s_t,a_t))$$
- $Q$ value = expected cumulative discounted reward
- cumulative discounted reward = $\Sigma_t \gamma^t r_t$ 
- $\alpha$ learning rate

### boltzmann distribution
- higher temperature $T$ -> higher stochasticity (randomness)
$$Pr(a)=\frac{e^{Q(s,a)/T}}{\Sigma_a e^{Q(s,a)/T}}$$

### model-based vs model-free
- model-based:
	- learn based on a model
	- faster training time
	- safe choice, less risky
- model-free:
	- no model, learn on what's better from previous actions taken
		- less complex
	- longer training time
	- can be very good if more training tho
	- good for unpredictable results

### deep-q network (DQN)
gradient q-learning:
- [[neural networks]]
- experience replay
	- sample previous experience in minibatch $(s,a,s',r)$
		- stable learning: correlation with past learnings
		- better data efficiency: less interactions to be done with env
- target network
	- separate network only updated periodically
		- mitigate divergence