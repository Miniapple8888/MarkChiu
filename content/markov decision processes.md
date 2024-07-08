
problem with supervised machine learning
- need a lot of labeled data
alternatives:
- unsupervised machine learning
- [[reinforcement learning]]

analogy to animal behaviours: 
animals learn through punishments (pain and hunger) and rewards (pleasure and food)

![reinforcement learning model](https://www.researchgate.net/publication/333884677/figure/fig2/AS:771670948212736@1560992099587/Basic-reinforcement-learning-model-When-the-Agent-performs-an-action-the-state-of-the.png)

industrial usage:
- contextual bandits
- bayesian optimization
- sequential decision making

ex:
playing go
- state: board config
- env: opponent
- agent: player
- action: next stone location
- reward: win +1/ lose -1

goal: long-term learning

components:
- states $s \in S$
- actions: $a \in A$
- rewards $r \in \mathbb{R}$
- transition model $Pr(s_t | s_{t-1} a_{t-1})$
- reward model: $R(s_t, a_t)=\Sigma_{r_t}r_t Pr(r_t | s_t a_t)$ 
- discount factor: $0 \leq \gamma \leq 1$
	- idea comes from game theory and macroeconomics
	- better to get reward now than later
	- used to calculate finite sum of reward
- horizon: $h \in \mathbb{N}$ or $h=\infty$ 

**stationary**: dependent of state
**non-stationary**: dependent of time and state
### common assumptions
- transition model
	- markovian
		- current inventory enough to predict future
	- stationary
		- demand is the same everyday
- reward model
	- stationary
		- formula is the same everyday
	- exception
		- terminal reward is different

goal: maximize total reward $R(s_t, a_t)=\Sigma_{r_t}r_t Pr(r_t | s_t a_t)$
sol 1. discounted reward
- discount factor $0 \leq \gamma \leq 1$
- reward becomes geometric sum: finite utility
- inflation rate: $\frac{1}{1-\gamma}$ 
sol 2. avg reward


## policy
choose action based on state $\pi (s_t)=a_t$
assumption: observable states

- policy evaluation: expected utility
	- $$V^{\pi}(s_0) =\Sigma^h_{t=0}y^t\Sigma_{s_{t+1}}Pr(s_{t+1} | s_0, \pi)R(s_{t+1},\pi (s_{t+1}))$$
- optimal policy $\pi^*$ highest utility
	- $$V^{\pi^*}(s_0) \geq V^{\pi}(s_0) \forall \pi$$
several algos:
- value iteration
- policy iteration
- linear programming
- search techniques

## bellman's equation
value iteration
$$V_{\infty}^*(s_t)=\max_{a_t}R(s_t, a_t)+\gamma \Sigma_{s_{t+1}}Pr(s_{t+1}|s_t,a_t)V_{\infty}^*(s_{t+1})$$

## horizon effect
- finite $h$
	- non-stationary effect
	- best action at different step
- infinite $h$
	- stationary effect
	- problem: value iteration infinite steps
		- after $n$ steps, $\gamma^n \to 0$ so reward become insignificant
	- solution:
		- pick large enough $n$ to run value iteration for $n$ steps, execute policy at $n$th step
		- iterate while $|| V_n - V_{n-1}|| < \epsilon$, execute policy at $n$th step
	- 