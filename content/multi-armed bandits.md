form of [[reinforcement learning]] with 1 state
## stochastic bandits
- single state ~ multiple states -> contextual bandits
- set of actions
- space of rewards [0,1] $R(a)$
goal: learn stochastic reward function

ex: try different slot machines at a casino to find the one with best payoff
payoff = probability click through add (pays) $\times$ amount paid

exploration: explore to see best options
exploit: use knowledge to 

## heuristics
- **greedy heuristic**: select highest avg so far. 
	- might get stuck due to lack of exploration
- **$\epsilon$ - greedy heuristic**: select arm at random or greedily
	- convergence rate (or how fast we find best arm) depends on $\epsilon$ 
## regret
$R(a)$ ~ unknown avg of reward for action $a$
$r^*=\max_aR(a)$ and $a^*=argmax_aR(a)$
expected regret of $a$
$$loss(a)=r^*-R(a)$$
expected cumulative regret of $a$ for $n$ steps
$$Loss_n=\Sigma^n_{t=1}loss(a_t)$$

## theoretical guarantees
when $\epsilon$ is constant:
- for large $t$ : $Pr(a_t \neq a^*) \approx \epsilon$
- expected cumulative regret: $Loss_n \approx \Sigma^n_{t=1}\epsilon=O(n)$
	- linear regret
when $\epsilon \propto 1/t$:
- for large $t$, $Pr(a_t \neq a^*) \approx \epsilon_t = O(\frac{1}{t})$
- expected cumulative regret: $Loss_n \approx \Sigma^n_{t=1}\frac{1}{t}=O(\log n)$
	- logarithmic regret

how far is empirical mean $\tilde{R}(a)$  from true mean$R(a)$
$$|\tilde{R}(a) - R(a)| < bound$$
upper bound: $R(a) < \tilde{R}(a) + bound$

### positivism in face of uncertainty
given oracle returns upper bound $UB_n(a)$ on $R(a)$ for $n$ trials of arm $a$
suppose upper bound converges to limit: $\lim_{n \to \infty} UB_n(a)=R(a)$ then
optimistic algo: select $argmax_a UB_n(a)$  at each arm

***theorem***: selecting $UB_n(A)$ will converge to $a^*$ 
can be proved by contradiction

problem: cannot compute upper bound because we are sampling
so we obtain measures of $f$ that approximates upper bound, using Hoeffding's inequality
$$Pr(R(a) - f(a)) \geq 1 - \delta$$

### hoeffding's upper bound algo
UCB will converge, try arms infinite amount of time
logarithmic regret


UCB algo performs better than $\epsilon$ greedy


## bayesian learning

$$Pr(\theta| r_1^a, r_2^a, ..., r_n^a) \propto Pr(\theta)Pr(r_1^a, r_2^a, ..., r_n^a|\theta)$$

## thompson sampling
sample several potential rewards
$$\tilde{R}(a) \sim Pr(R(a)|r_1^a, ..., r_n^a)$$
execute $argmax_a \tilde{R}(a)$ 
expected cumulative regret $O(\log n)$

in practice, thompson often outperforms UCB and $\epsilon$ greedy