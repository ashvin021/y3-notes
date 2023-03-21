- This stands for Scale Invariant Feature Transform Descriptor
- We can use these descriptors for [[Keypoint Matching]].
- Steps:
	1. **Detection of scale-space extrema**
		- We use a [[Difference of Gaussian]] filter to indentify potential interest points (we search across scales and pixel locations)
			- This is implemented by calculating a stack of Gaussian smoothed images, then calculating their differences
				- $\text{DoG}(k^3 \sigma) = G(k^4 \sigma) - G(k^3 \sigma)$
			- eg: $k = \sqrt{2}$ gives us $\sigma, \sqrt 2 \sigma, 2 \sigma, 2\sqrt 2 \sigma, 4 \sigma$
		- We use the term extrema here, because we're looking at both minima and maxima
	2. **Keypoint localisation**
		- We want to refine the localisation and scale for the extrema in order to achieve sub-pixel accuracy.
			- In other words, the 'true' extrema might be at some sub-pixel point; we want to find it.
		- **Method**: A quadratic function is fitted to the DoG response of the neighbouring pixels. Then the location and scale of extremum for this quadratic function can be estimated.
			- Denote the DoG response by $D(x, y, \sigma)$ or $D(\mathbf{x})$, where $\mathbf{x} = (x, y, \sigma)^T$ is a 3D vector containing both location and scale.
			- Taking the Taylor Expansion, we get: $$D(\mathbf{x} + \Delta\mathbf{x}) = D(\mathbf{x}) + \frac{\delta D^T}{\delta x}\Delta x + \frac{1}{2}\Delta x^T \frac{\delta^2 D}{\delta x^2} \Delta x$$
				- The first derivatives can be estimated using finite difference, eg: $$\frac{\delta D}{\delta \mathbf{x}} = \frac{D(\mathbf{x} + 1, y, \sigma) - D(\mathbf{x} - 1, y, \sigma)}{2}$$
				- The second derivatives or [[Hessian]] can be estimated using finite difference as well.
			- To estimate a refined e\mathbf{x}trema for this function, we can let $$\frac{\delta D(\mathbf{x} + \Delta \mathbf{x})}{\delta \Delta \mathbf{x}} = \frac{\delta D}{\delta \mathbf{x}} + \frac{\delta^2 D}{\delta \mathbf{x}^2}\Delta \mathbf{x} = 0$$
			- Therefore, $$\Delta \mathbf{x} = -\frac{\delta^2 D^{-1}}{\delta \mathbf{x}^2} \frac{\delta D}{\delta \mathbf{x}}$$
			- We move from $\mathbf{x}$ by $\Delta \mathbf{x}$ and arrive at the refined estimate.
			- [[CV Cheatsheet]]
	3. **Orientation assignment**
		- We need to know the scale and orientation at the keypoint. Scale is already known when we detect the keypoint (through the DoG value for $\sigma$ and keypoint localisation).
		- **Idea**: Find the dominant orientation for a keypoint.
		- **Implementation**:
			1. An orientation histogram with 36 bins covering 360 degrees is created.
			2. Each pixel's gradient orientation votes for an orientation bin, weighted by the gradient magnitude.
			3. The keypoint will be asigned an orientation corresponding to the maximum of the histogram.
		- Diagram:
			- ![[Pasted image 20230319200737.png|300]]
	4. Keypoint descriptor
		- **Idea**: we draw sample points in the local region, calculate their gradient orientations, and form a histogram. 
			- This is done in a scaled coordinate system based on the orientation assignment for rotational invariance.
			- ![[Pasted image 20230319200630.png]]
		- **Implementation**:
			1. Divide the area arount the keypoint into 16 subregions (Lowe's Implementation), to describe features at different parts of the local area
			2. Within each subregion, a number of points are sampled and a histogram is formed
		- The dimentions of the above descriptor are: 128 = 16 subregions $\times$ 8 bins
		- We use a *feature vector of 128 elements* to describe each keypoint.
		- ![[Pasted image 20230319200330.png]]