### Unsupervised
- Thresholding
	- At each pixel $x$, the label is defined by, $$f(x) = \begin{cases}1 & \text{if} \  I(x) \geq threshold \\ 0 \ \text{otherwise} \end{cases}$$where $I(x)$ is the intensity of the pixel.
- K-Means Clustering
- Gaussian Mixture Model
	- **Problem**: K-Means performs a hard assignment of data point $x$ to cluster $k$.
	- **Idea**: GMM performs a soft assignment by assuming a Gaussian distribution for each cluster.
	- The probability that $x_j$ belongs to cluster $k$ is$$P(y_j = k|x_j, \pi_k, \mu_k, \sigma_k) = \pi_k \cdot \frac{1}{\sqrt{2\pi}\sigma_k}\exp{\left(-\frac{(x_j - \mu_k)^2}{2\sigma_k^2}\right)}$$
		- $x_j$ - The intensity of feature for data point $j$
		- $y_j$ - Class for data point $j$
		- $\pi_k, \mu_k, \sigma_k$ - Parameters for cluster $k$


### Supervised
- Convolutional Neural Network