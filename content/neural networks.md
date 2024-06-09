Some notes taken from [CS486](https://cs.uwaterloo.ca/~wenhuche/teaching/cs486-2024/)
# terminology
- neuron:
	- 🔥 fires (activates) when $\Sigma_{i=1}^n (a_i \cdot w_i + b_i) > \text{threshold}$
	![[neuron-neural-network.png]]
	- $in_j = \Sigma_{i=1}^n (a_i \cdot w_i + b_i)$ : input signal
		- $a_i$ : activation/input of previous layer
		- $w_i$: weight (edge) associated to activation - strength of connection
		- $b_i$: bias associated to activation
		- $n$ : number of activations/neurons in previous layer
	- $g(in_j)$ : activation function applied on input signal (is the threshold)
		- properties:
			- should be nonlinear. cannot get nonlinear from combination of linear.
			- mimic real neurons: fire 1 if activated, 0 else.
			- differentiable almost everywhere: so we can use optimization algo like gradient descent
		- common activation functions
			- step function: $g(x) = 1$ if $x > 0$ else $0$ 
				- not differentiable, but simple.
			- sigmoid function: $g(x)=\frac{1}{1+e^{-kx}}$
				- can finetune param $k$ to mimic step function
				- vanishing gradient problem:
					- as $k$ -> large: 
				- computationally expensive 💰
				