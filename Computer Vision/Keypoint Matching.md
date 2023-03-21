1. Find the nearest neighbours of the descriptors
	- For each keypoint in image $A$, indentify its nearest neighbours in the set of keypoints for image $B$.
	- For [[SIFT Descriptor]]s, we use the Euclidean Distance.
	- We can find approximate nearest neighbours for efficiency.
2. Use an affine model to map a keypoint $(x, y)$ in image $A$ to another keypoint $u, v$ in image $B$.
	- $$\colv{u \\ v} = \mat{m_1 & m_2 \\ m_3 & m_4} \cdot \colv{x \\ y} + \colv{t_x \\ t_y}$$
		- Here, $m_{1\dots4}$ are used for rotation and scaling, and $t_x$ and $t_y$ are usde for translation.
	- We can write this as a linear system, $Am = b$, where $m$ is the vector of unknown affine parameters, with the form: $$\matrix{x_1 & y_1 & 0 & 0 & 1 & 0 \\ 0 & 0 & x_1 & y_1 & 0 & 1 \\ x_2 & y_2 & 0 & 0 & 1 & 0 \\ 0 & 0 & x_2 & y_2 & 0 & 1 \\ & & \vdots & & } \cdot \colv{m_1 \\ m_2 \\ m_3 \\ m_4 \\ t_x \\ t_y} = \colv{u_1 \\ v_1 \\ u_2 \\ v_2}$$
	- The least-square solution to the linear system is given by, $$m = (A^T A)^{-1} A^T b$$which minimises the squared difference $\|Am - b\|^2$ 
	- Once the affine parameters are solved, we know the spatial transformation between the two images.
3. We solve the affine model using [[RANSAC]] instead of using all the keypoints, in order to deal with outliers.
	- In this case:
		- *Distribution sampled from*: All the matched keypoint pairs
		- *Model to fit*: Affine model that maps transformation