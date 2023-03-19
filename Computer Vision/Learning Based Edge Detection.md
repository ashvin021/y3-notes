- It assumes that paired data (images $x$ and manually defined edge maps $y$) are available
- The problem becomes how to find a model $f$ that maps $x$ to $y$, i.e. $f(x|\theta) = y$ where $\theta$ denote the model's parameters.
- In the below example, the machine learning model integrates features from multiple scales, fusing fine-scale edges with course-scale edges to form the final output.
- On the contrary, [[Canny Edge Detection]] only uses a single scale for edge detection, controlled by Gaussian parameter $\sigma$.
 
![[Pasted image 20230319013802.png|450]]