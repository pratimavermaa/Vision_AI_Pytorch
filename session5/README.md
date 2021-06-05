
## Team ##

* Praveen Pethurajan
* Ashwin Aralamallige Gopalakrishna
* L.Mahesh
* Pratima Verma

### Session 5 Assignment ###

### Iteration 1

### Target
Light network with <8K parameters

### Result

*   Parameters: 7,702
*   Best Train Accuracy: 98.5
*   Best Test Accuracy: 98.5

### Analysis

*   Good model(not best) with less number of parameters. Less than 8K params.
*   Not over-fitting. Model is capable of getting trained further.

### Iteration 2

### Target
Add batch normalization

### Result

*   Parameters: 7,854
*   Best Train Accuracy: 99.6
*   Best Test Accuracy: 99.2

### Analysis

*   This models start to over-fit after 3rd epoch itself. 
*   Should avoid over-fitting. Model can be pushed further by adding regularization.

### Iteration 3

### Target
Add Regularization

### Result

*   Parameters: 7,854
*   Best Train Accuracy: 99.4
*   Best Test Accuracy: 99.3

### Analysis

*   Added dropout layers
*   The gap between thet training accuracy and test accuracy reduced. 
*   The model is not overfitting. Need to push the model further to make training harder.

### Iteration 4

### Target
Add image augmentation by introducing random rotation

### Result

*   Parameters: 7,854
*   Best Train Accuracy: 99.2
*   Best Test Accuracy: 99.5

### Analysis

*   The training got harder which resulted in decrease in training accuracy compared to the previous model.
*   Can see an improvement in test model accuracy and it is around 99.4 consistently in the last 4 epochs.
