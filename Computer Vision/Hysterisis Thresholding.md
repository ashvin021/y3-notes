- Hysterisis Thresholding defines two thresholds $t_{low}$ and $t_{high}$ for [[Edge Detection]].
- Method:
	- If a pixel's [[Gradient Magnitude]] is $\geq t_{high}$, it is accepted as an edge pixel. 
	- If it is lower than $t_{low}$, it is rejected.
	- If it is in between, it is a weak edge pixel. It may or may not be an edge pixel.
		- We check its neighbouring pixels. It will be accepted if it is connected to an edge pixel.
		- We iteratively perform this check until all pixels are either accepted or rejected.

![[Pasted image 20230319021258.png]]
![[Pasted image 20230319021315.png]]