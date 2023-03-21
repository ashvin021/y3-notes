### Algorithm
1. Compute the $x$ and $y$ derivatives of the image, $$I_x = G_x \ast I \qquad I_y = G_y \ast I$$where $G$ can be the [[Sobel Filter]].
2. At each pixel, compute the matrix $M$, $$M = \sum_{x, y} w(x, y) \begin{bmatrix}I_x^2 & I_x I_y \\ I_x I_y & I_y^2\end{bmatrix}$$
3. For each pixel, calculate the cornerness score, $$R = \lambda_1\lambda_2 - k(\lambda_1 + \lambda_2)^2 = \det(M) - k(\text{trace}(M))^2$$
4. Detect interest points which are local maxima (thought: possibly using [[Non-Maximum Suppression]]?), and whose response $R$ are above a threshold.

### Pros & Cons
- Pros
	- It is rotation-invariant
- Cons
	- This detector finds strong responses not only at corners, but also at blobs and textures
		- ![[Pasted image 20230319040316.png]]
	- It is not scale-invariant