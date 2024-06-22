recall: 3 types of machine learning
1. supervised learning -> given labels
2. unsupervised learning -> no label
3. reinforcement learning -> in between (has numeric feedback: rewards & punishments)

modeled as a Markov decision process:
- single agent given states $S$ and possible actions $A$
- each timestep, observe state + reward -> do action
	- assume full observability
- goal: maximize discounted reward over time

RL is hard:
- reward is infrequent
	- difficult to determine which action cause reward/lead to win/loss
- action long term utility

tradeoff explore or exploit