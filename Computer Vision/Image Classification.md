### How does image classification work?
- Pipeline
	- ![[Pasted image 20230319235045.png]]
	- *Feature extraction* - Transform input images into low-dimensional vectors so they can be easily compared and matched
	- *Classifier* - Trained with a dataset consisting of images and labels (or even without labels)
- We generally split the data into two parts:
	- *Training set* - For training the classifier
	- *Test set* - For evaluating the performance of the classifier on unseen data
	- We also sometimes split the training set into the training and *validation* set, in order to perform [[Hyperparameter Tuning]]
- Pre-processing
	- Removing other factors that we don't want the machine model to learn
	- Eg: MNIST providing a regular dataset and a deslanted dataset

### Feature Extraction
- Hand crafted
	- Eg: Pixel intensities, [[Histograms of Oriented Gradient (HOG)]] or another manually defined feature descriptor
- Learnt Features
	- Eg: Using [[Convolutional Neural Network]]s or another feature automatically learnt by the algorithm

### Classifiers

##### KNNs
![[K Nearest Neighbours (KNNs)]]

##### Support Vector Machines
![[Support Vector Machine]]

##### Neural Networks
![[Neural Network]]



##### Convolutional Neural Networks (CNN)
![[Convolutional Neural Network]]

##### Transformer

