game: 
- involves 2 or more self-interested, rational players
types of games:
- competitve
- cooperative
- both
components
- agents $N \ge 2$
- actions - strategy profile - set of joint actions
- reward function for each agent
	- cooperative: reward for agents are same
	- competitive: sum of rewards for each agent is zero
- no state
- horizon=1

types of games
 - coordination games: need to choose same strategy -- prisoner's dilemma

### dominated strategies
- $\exists a_i' \forall a_{i-1},R_i(a_i, a_{-i}) < R(a_i',a_{-i})$
- rational agents will not play strictly dominated strategies

### nash equilibrium
- agent's response depends on other agents' strategies
- $\forall i, a_i, R_i(a_i^*,a_{-i}^*) \ge R_i(a_i,a_{-i}^*)$
- strategy profile $a^*$ given that other agents don't deviate from their strategies
- strategy $a^*$ is nash equilibrium iff $\forall i, a_i^*=argmax_{a_i}R_i(a_i,a_{-i}^*)$

### mixed nash equilibria

# multiple agent reinforcement learning
- agents play at same time
	- no communication among agents
	- no observation
- choose one of the strategies