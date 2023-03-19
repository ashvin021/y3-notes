- Steps in the Canny Edge Detection Algorithm
	1. Perform [[2D Gaussian Filter|Gaussian Filtering]] to suppress noise
	2. Calculate the [[Gradient Magnitude]] and [[Gradient Orientation]].
		- [[Prewitt Filter|Prewitt]] or [[Sobel Filter|Sobel]] filtering can be applied.
	3. Apply [[Non-Maximum Suppression]] to get a single response for each edge.
	4. Perform [[Hysterisis Thresholding]] to find potential edges.


- Goals of the Canny Edge Detection Algorithm and how they are achieved
	1.  Good detection
		- Use Gaussian Filtering to suppress noise (reduces false positives).
		- Use Hysterisis Thresholding to find weak edges (reduces false negatives).
	2.  Good localisation
		- Use Gradient Orientation and Non-Maximum Suppression to find the location of edges.
	3.  Single Response
		- Non-Maximum Suppression.