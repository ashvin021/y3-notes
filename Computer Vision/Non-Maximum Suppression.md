> $$M(x, y) = \begin{cases} M(x, y) & \text{if local maximum} \\ 0 & \text{otherwise} & \end{cases}$$

- Aim: To get a single response for an edge
- Idea: Edge occurs when the [[Gradient Magnitude]] reaches the maximum.
- Solution:
	- Check whether a pixel $q$ (shown in diagram below) is a local maximum along the [[Gradient Orientation]]
	- We move to pixel $r$ and $p$, and compare the gradient magnitudes between the 3.
	- If $q$ is a local maximum, it is an edge-point and we suppress the other pixels, i.e. non-maximum pixels
- Implementation:
	- In implementation we need to perform image interpolation for pixels $p$ and $r$ if they are not on the pixel lattice
		- Using nearest neighbour or linear interpolation
	- Alternatively, we can round the gradient into 8 possible angles 
		- (0, 45, 90, 135, 180, 225, 270, 315)
		- We only check along these directions, so no interpolation is needed

|![[Pasted image 20230319015729.png\|300]]|![[Pasted image 20230319020036.png\|300]]|
|---|---