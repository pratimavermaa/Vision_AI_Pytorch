# Neural Network Training Overview

Consider a simple NN with two inputs, a hidden layer with two neurons and two outputs. The architecture is shown below:

![A simple Neural Network](/images/network_arch.jpg)

### What constitutes training this network?

It can be best expressed through a free flow pseudo code

``` 
for each epoch
	for each minibatch
		do forward pass
		compute error
		backpropogate gradients
		update weights
	record accuracy metrics
```

#### Major Steps

Let us talk a bit on the four major steps that happen for each minibatch.

1. __Forward Pass:__
	During the forward pass, the input signals are multiplied with weights and acted upon by activation functions to arrive at the outputs of the network. In the above case, a_o1 and a_o2 are computed from i1 and i2.

	During this process, it also works well to compute local gradients for each layer eg: d(a_h1)/dh1, d(o1)/da_h1, d(a_o1)/do1

2. __Compute Error/loss:__
	The error is obtained by applying the pre-decided loss function to quantify the difference between the ground truth/target and the output of network we obtain in the current epoch. For our example, we have considered the squared loss function which is given by:

	![Squared Error Loss](/images/loss_fn.png)

3. __Backpropogate Gradients:__
	Let's think about our NN as a computational graph. Hence, we want to make the gradient of the error flow from the output to the input layer using the computed local gradients. The flowing of gradient simply means chaining products of gradients according to chain rule. For eg, we propogate d(E_total)/da_o1 till the input layer, till i1

	We then have the gradients at each layer .i.e. d(E_total)/doutput_nodes and d(output_nodes)/dhidden_nodes

4. __Update weights:__
	Finally, we can now update the weight by using the gradient at the node to which the weight connects to .i.e. its closest node. This is again a direct application of chain rule. For example, for w1 this would be the gradient at h1 multiplied by gradient of h1 wrt w1.

	![Gradient for weight w1](/images/gradient_w1.png)

	Once we have the gradient of error wrt each weight, we can go ahead and make an update to each weight of the network:

	![Weight Update](/images/weight_update.png)

### Results

The excel file can now be used to emulate the training process, albeit for a fixed input. However, we can clearly see how gradient descent updates minimize the Error/loss in subsequent iterations.

![Training snapshot](/images/training.jpg)

We can also investigate how learning rate affects the training process as shown below.

![Learning Rate](/images/lr.png)

Clearly, an increase in learning rate is leading to a faster reduction in the overall error of the network. However, we must keep in mind that larger learning rate values may cause SGD to not coverge to the minima desired. Moreover, very large values of lr lead to the violation of applicability of partial derivatives, the primary principle behind gradient descent.

One can play around with the backprop.xlsx to better understand gradient descent, forward and backprop along with the overall training of a Fully Connected NN 


