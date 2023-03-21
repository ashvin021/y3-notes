- Problem: How do we describe the local feature or content around a point?
	- Simple Descriptors
	- SIFT Descriptor

### Simple Descriptors
1.  Pixel Intensity
	- Simply using the intensity of a single pixel
	- Problems
		1.  Sensitive to absolute intensity value
			- The intensity of the same point will change under different illuminations
		2.  Not very descriminative
			- Small range of pixel intensities (0 to 255 in grayscale)
			- Does not represent any local content
2. Patch intensities
	- Take the intensities of a patch around the point
	- Benefits
		1. Represents the local pattern
		2. Performs well if the images are of similar intensities and roughly aligned
	- Problems
		1. Sensitive to absolute intensity value
		2. Not rotation-invariant
3. Gradient orientation
	- Use horizontal and vertical Sobel fiters and use `atan2` to obtain the gradient orientation
	- Benefits
		1. Robust to change of absolute intensity values
	- Problems
		1. Not rotation-invariant
		2. Not scale-invariant
4. Histogram
	- The histogram of pixel intensities in a patch
	- Benefits
		1. Robust to rotation
		2. Robust to scaling
	- Problems
			1. Sensitive to intensity changes

### SIFT (Scale-Invariant Feature Transform) Descriptor
![[SIFT Descriptor]]

### SURF
![[SURF Descriptor]]

### BRIEF
![[BRIEF Descriptor]]

### HOG
![[Histograms of Oriented Gradient (HOG)]]

