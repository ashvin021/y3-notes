- This is the simplest form of an [[Artificial Neuron]], and was developed by Frank Rosenblatt in 1957.
- It consists of only a single later, and uses the Heaviside Step Function as an activation function.

$$y = \begin{cases}1 & \text{if}\ \mb{w} \cdot x + b > 0 \\ 0 & \text{otherwise}\end{cases}$$
- We optimise $\mb{w}$ and $b$ so that $y$ matches ground truth.

![[Pasted image 20230320030047.png|400]]