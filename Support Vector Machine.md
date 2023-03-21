- In its simplest form ([[Linear SVM]]), it is a line that separates two different classes.
- For general cases, the linear model is formulated as: $$\mathbf{w} \cdot \mathbf{x} + b = 0$$
	- $\mathbf{w}$ - the weights, normal
	- $\mathbf{x}$ - data, feature
	- $b$ - bias
- The rule of the linear classifier is to assign a class $c$ to data $x$, $$c = \begin{cases}+1 & \text{if} \ \mathbf{w} \cdot \mathbf{x} + b \geq 0 \\ -1 & \text{otherwise} \end{cases}$$
- To train the classifier, we estimate model parameters $\textbf{w}$ and $b$.
- In order to do this, we want to find the **Maximum Margin Hyperplane**. 

#### Determining the Maximum Margin Hyperplane
- To determine the maximum margin hyperplane, we only need the innermost points, which are called the **support vectors**.
	- We would like the support vectors to fulfill the equations $\mathbf{w} \cdot \mathbf{x} + b = 1 \ \text{or}\  -1$, so that all other points are easily classified.
	- We would also like to maximse the margin between the dashed lines.
	- ![[Pasted image 20230320014830.png|400]]
- The margin is, $$m = \frac{2}{\|w\|}$$
	- Derivation:
		- Let $\mathbf{x}_1$ be a point on the plane $\mb{w} \cdot \mb{x} + b = -1$, we have $\mb{w} \cdot \mb{x}_1 + b = -1$. 
		- Move $\mb{x}_1$ along the normal direction $\mb{n}$ for the distance of the margin $m$, it will arrive at the point $\mb{x}_2$ on the other plane $\mb{w} \cdot \mb{x} + b = 1$
		- $\mb{w} \cdot (\mb{x}_1 + m\mb{n}) + b = 1$
		- We have $m\mb{w} \cdot \mb{n} = 2$
		- Since $\mb{n} = \frac{w}{\|w\|}$, we have that $m = \frac{2}{\|w\|}$
- Maximising the margin can be re-formulated as an optimisation problem, $$\min_{\mb{w}, b}\|w\|^2$$subject to $y_i(\mb{w}\cdot\mb{x}_i + b) \geq 1$ for $i = 1, 2, \dots, N$
	- This is a quadratic optimisation problem subject to linear constraints
	- This is done by using the value of $y_i$ to unify the two classes.
- This can further be re-formulated as, $$\min_{\mb{w}, b}\|w\|^w + C\sum_{i = 1}^N{\max(0, 1 - y_1(\mb{w} \cdot \mb{x}_i + b))}$$
	- The second term is called the *hinge loss*, $$h = \max(0, 1 - y_i(\mb{w} \cdot \mb{x}_i + b))$$
	 - [[CV Cheatsheet]]
- We optimise this loss function using [[Gradient Descent]].
	- We calculate the gradient w.r.t $\mb{w}$ and $b$ separately, in order to optimise them both.
	- ![[Pasted image 20230320022657.png|500]]
	- ![[Pasted image 20230320022715.png|500]]
- We can use [[Stochastic Gradient Descent]] since it would be computationally expensive to evaluate the gradient over the whole training set.

#### How do we perform multi-class classification?
- **One vs Rest Strategy**
	- Train a classifier for each of the $K$ classes
		- $c_1$ vs others, $c_2$ vs others, $c_3$ vs others, ...
	- During testing, apply all $K$ classifiers to the test data.
	- The classifier which produces the highest response will determine the result.
		- $$c = \text{argmax}_{k = 1, 2, \dots, K}f_k(\mb{x})$$where $f_k(x) = \mb{w}_k \cdot \mb{x} + b_k$ denotes the k-th classifier.
- **One vs One Strategy**
	- Train a classifier between each pair of classes
		- For all $i$, $j$ we have classifier between $c_i$ and $c_j$.
	- For $K$ classes, we need $\frac{K(K - 1)}{2}$ classifiers.
	- At test time, each classifier will vote for a class.
	- Count the vote for each class and perform majority voting.
 