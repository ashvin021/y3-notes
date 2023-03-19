1. Perform smoothing
	- This helps suppress noise, so edges are easier to detect.
	- Smoothing is part of the [[Prewitt Filter]] (moving average) and the [[Sobel Filter]] (weighted average).
	- Another option is to use a [[2D Gaussian Filter]] to perform smoothing, and then perform edge detection with a Prewitt or Sobel filter.
		- The larger the $\sigma$ used in the Gaussian smoothing, the thicker the detected edges will be.
		- This is because a larger $\sigma$ suppresses more noise.
 2. Get the horizontal and vertical derivatives with the [[Prewitt Filter]] or [[Sobel Filter]]
 3. Calculate the gradient magnitude at each pixel to create an edge map.
	 - ![[Gradient Magnitude]]
 4. Gradient orientations can also be calculated as follows:
	 - ![[Gradient Orientation]]