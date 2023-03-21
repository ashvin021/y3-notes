- **Idea**: We can do object detection in two stages
	1. Stage 1: Initial guess, propose some possible regions of interest
	2. Stage 2: perform classification and localisation for these regions

### Faster R-CNN 
- *Steps*:
	1. A [[Region Proposal Network]] is applied to the convolutional feature map to propose possible regions of interest.
		- A **convolutional** feature map is the result of a convolutional layer.
			- Here it is provided by a **backbone network** (AlexNet or VGG-16), which are often pre-trained on ImageNet or other datasets.
			- Each pixel of the feature map is a high dimensional feature vector, which may tell whether this is an interesting region or not.
			- ![[Pasted image 20230320235131.png|400]]
		- To propose regions, we,
			1. Go across the feature map using a 3x3 sliding window.
			2. Using features at this window, we perform a binary classification (0 - not interesting, 1 - interesting)
			3. At each sliding window, the network makes $k$ predictions, for objects of different scales and aspect ratios.

- One-stage vs two-stage detection methods

