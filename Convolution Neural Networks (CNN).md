
A type of deep learning algorithm used to analyze visual data, designed to mimic the human cortex.

Neural network layers:
- Input layer
- one or more hidden layers
- output layer

Each node connects to another and has a line weight and threshold value. If the data in the node passes the threshold value it is transferred to the next layer in the network. 

In a CNN, each layer increases in complexity where earlier layers focus on simpler features.

CNN layers:
- Convolutional layer
	- Input data - image made of a matrix of pixels (height, width, depth)
	- Filter - a kernel that move across the image to check whether a feature is present (known as convolution) (3x3 matrix of weights that shifts by a stride)
	- Feature map - the final output of input image times the dot product of the filter
- Pooling layer
	- Down samples to reduce complexity and limit overfitting. 
- Fully-connected (FC) layer
	- This layer actually does the classification using the features using the previous layers. Use a SoftMax or sigmoid. 

Fixed values that are not changed by back propagation
- Number of filters
- Stride
- Padding

The CNN applies a Rectified Linear Unit (ReLU) function to the feature map to introduce nonlinearity?

