### Concept
- Basic Idea:
	- Look at a small window of pixels, to tell the difference between edge pixels and corner pixels
	- Shift the window and calculate the change of intensities for the window
		- *Edge*: change of intensity along just one direction
		- *Corner*: change of intensity along both directions
		- *Flat region*: no change in any direction
	- If the window $W$ shifts by $[u, v]$ , the change of intensities is given by: $$E(u, v) = \sum_{(x, y) \in W} w(x, y) [I(x + u, y + v) - I(x, y)]^2$$ where $E(u, v)$ is the sum of squared differences between the two windows.
		- Further explanation of terms
			- $E(u, v)$ - sum of squared differences
			- $w$ - window function, this can be a discrete (1 in window, 0 outside) or a [[2D Gaussian Filter|Gaussian]] window
			- $I(x + u, y + v)$ - intensity of the shifted window
			- $I(x, y)$ - original intensity
			- ![[Pasted image 20230319024719.png]]
---
- For a small shift $[u, v]$, we have the following bilinear approximation, $$E(u, v) \approx [u, v] \cdot M \cdot \colv{u \\ v}$$ where $M$ is a $2 \times 2$ matrix, computed from the image derivatives, $$M = \sum_{x, y} w(x, y) \begin{bmatrix}I_x^2 & I_x I_y \\ I_x I_y & I_y^2\end{bmatrix}$$
	- Derivation:
		- Taylor expansion of $I(x + u, y + v)$,  $$I(x + u, y + v) = I(x, y) + uI_x(x, y) + vI_y(x, y) + \dots$$
		- If we use first order approximation, we get $$\begin{align*} E(u, v) &= \sum_{(x, y) \in W} w(x, y) [I(x + u, y + v) - I(x, y)]^2 \\  \\ &\approx \sum_{(x, y) \in W} w(x, y) [uI_x(x, y) + vI_y(x, y)]^2 \\ \\  &= \sum_{(x, y) \in W} w(x, y)[u^2I_x^2 + 2uvI_xI_y + v^2I_y^2] \\ \\ &= \sum_{(x, y) \in W} w(x, y)[u, v] \begin{bmatrix}I_x^2 & I_x I_y \\ I_x I_y & I_y^2\end{bmatrix}\colv{u \\ v} \\ \\ &= [u, v] \sum_{(x, y) \in W} w(x, y) \begin{bmatrix}I_x^2 & I_x I_y \\ I_x I_y & I_y^2\end{bmatrix} \colv{u \\ v} \end{align*}$$

	- We will get a large $M$ when the derivatives are large
	- $M$ is a $2 \times 2$ matrix, so we can infer the directions of change by $M$.
---
- Since $M$ is a real symmetric matrix, it can be represented by the following through eigen decomposition: $$M = P \Lambda P^T$$
	- $\Lambda$ is a diagonal matrix with the eigenvalues of $M$ as below, $$\Lambda = \begin{bmatrix}\lambda_1 & 0 \\ 0 & \lambda_2\end{bmatrix}$$
	- If $\lambda_1 = \lambda_2 = 0$, it is a *flat region*.
	- If $\lambda_1 >> \lambda_2$ or $\lambda_2 >> \lambda_1$, it is an *edge*.
	- If $\lambda_1$ and $\lambda_2$ are both non-zero and of similar magnitude, a *corner* has been detected.
	- ![[Pasted image 20230319033702.png]]

### Defining Cornerness
- Harris and Stephens (1988) ([[Harris Detector]]), $$R = \lambda_1 \lambda_2 - k(\lambda_1 + \lambda_2)^2$$where $k$ is a small number, eg $k = 0.05$.
	- Alternative definition: $$R = \det(M) - k(\text{trace}(M))^2$$
	- Explanation:
		- This uses the fact that $$\det(M) = \det(P\Lambda P^T) = \det(\Lambda) = \lambda_1 \lambda_2$$ since $\det(AB) = \det(A)\det(B)$, and that $$\text{trace}(M) = \text{trace}(P\Lambda P^T) = \text{trace}(\Lambda) = \lambda_1 + \lambda_2$$ since $\text{trace}(AB) = \text{trace}(BA)$.

- Other definitions:
	- Kanade and Tomasi (1994), $$R = \min(\lambda_1, \lambda_2)$$
	- Noble (1998), $$R = \frac{\lambda_1 \lambda_2}{\lambda_1 + \lambda_2 + \epsilon}$$