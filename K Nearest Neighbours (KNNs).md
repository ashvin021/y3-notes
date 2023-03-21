- This is a non-parametric classifier.
	- This means that it depends only on the input data, and has no learnable parameters (in contrast to a [[Neural Network]]).
- If $k = 1$, each test data point is assigned the class of its nearest neighbour.
- If $k > 1$, we compute the K Nearest Neighbours and assign the class by majority voting.

### Distance Metrics
![[Distance Metrics]]

### Hyper-Parameters
- K is the only hyper parameter for a KNN.
- We optimise this using [[Hyperparameter Tuning]], and must make sure to use [[Cross Validation]] when doing this.

### Pros & Cons
- Pros
	- No training time
	- Simple but effective
	- Multi-class classification
- Cons
	- Storage and search are expensive - all the data needs to be stored and searched through
