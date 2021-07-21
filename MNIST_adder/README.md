# Pytorch MNIST plus adder network

The goal here is to build a dataset, loader and training module to train a simple network that:
1. predicts the digit from MNIST dataset
2. Sums said digit to a random number and predicts the output

### Data representation

The image input is straightforward and maintained as a 1x28x28. The random number is converted to a one hot vector.
This means 1 is converted to [0,1,0,0,0,0,0,0,0,0] while 9 would be represented as [0,0,0,0,0,0,0,0,0,1]

### Data generation

The two representations have been built into an abstraction of the Dataset class as shown below:

```python
# create the Dataset class
from torch.utils.data import Dataset

class MNIST_number(Dataset):
  def __init__(self, mnist_set):
    # use MNIST data
    self.image_data = mnist_set
    self.length = len(mnist_set.train_labels)
    # create a random number
    self.rand_nos = torch.randint(high = 10, size = (self.length, 1))
    self.one_hot_rands = F.one_hot(self.rand_nos)
  
  def __getitem__(self, index):
    # return data and labels for both the MNIST digit detector and random number generator
    image_sample, image_label = self.image_data[index]
    number_sample = self.one_hot_rands[index]
    number_label = self.rand_nos[index].item()
    return (image_sample, number_sample), (image_label, number_label+image_label)

  def __len__(self):
    return self.length

train_set = MNIST_number(train_mnist_set)
```

### Combination of inputs

The forward pass on the network has been improvised. First, the image data is run through a few CNN layers to arrive at the prediction of the shape [-1, 10]. Now, the random numbers are concatenated with this tensor and they also are of shape [-1, 10]. Hence this results in a tensor of shape [-1,20]. This is now fed to a series of fc layers ultimately resulting in two outputs of shape [-1,10] & [-1, 19] which represent the digit and its sum with a random number respectively

### Loss

The loss that was chosen is categorical cross entropy for both the digit recognition and sum prediction, since both outputs are one hot vectors. The resulting components were then summed together to obtain total loss.

Backward propagation is now performed on this total loss and the weights were updated based on the gradients using the Adam optimizer.

### Results

We see that the training performs well for MNIST but lands at a 50pc accuracy for the sum prediction. This needs to be explored further but the logs elucidate this in the best manner!

![Training Logs](/training_logs.JPG)

Authors
=====
Ashwin Aralamallige Gopalakrishna </br>
L.Mahesh </br>
Pratima Verma </br>
Praveen Pethurajan </br>