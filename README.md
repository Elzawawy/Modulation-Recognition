# Problem Statment 
DeepSig Dataset: RadioML 2016.04C
A synthetic dataset, generated with GNU Radio, consisting of 11 modulations. This is a
variable-SNR dataset with moderate LO drift, light fading, and numerous different
labeled SNR increments for use in measuring performance across different signal and
noise power scenarios. 

# About Data 
Data version used is available from [here](http://opendata.deepsig.io/datasets/2016.10/RML2016.10b.tar.bz2).

Every sample is presented using two vectors each of them has 128 elements. The dataset has the signals with raw features so we extracted more features
from it which are:

○ First Derivative in Time

○ Integral in Time

We used extracted features and created a combination of them in order to
have more datasets with different features to train the model, the
combinations are:

○ Derivative Features + Raw Features

○ Integral Features + Raw Features

○ Integral Features + Derivative Features

○ Integral Features + Derivative Features + Raw Features

As the size of datasets with the combination of features was very large to fit b in the memory, we converted them to **T
ensorflow Records** so we can train the model with data loaded on disk. Each dataset is splitted into 50% for training/validation and 50% for testing

# Fully connected Model Approach 
**Architecture used for the FCN is:**

○ Input layer of size (2,128)

○ First hidden layer of size 512

○ Second hidden layer of size 512

○ Flatten Layer

○ Softmax output layer of size 10

Activation function of neurons is ReLU. The optimizer used is Adam. The loss function used is Categorical Cross Entropy.

**Results: **

Best model from this approach was the one using the first derivative in time and raw features combination and scored a 45.86% testing accuracy in the evaluation. 

# Convolutional Neural Network Model Approach 

**Architecture used for CNN:**

○ Input layer of size (128,2,1)

○ Convolutional layer with 64 filters of size (3,1)

○ Max Pooling Layer

○ Convolutional Layer with 16 filters of size (3,2)

○ Flatten Layer

○ Dropout Layer

○ Fully connected layer of size 128

○ Softmax output Layer

**Results:**

Best model fromn this approach was the one using the integral in time features and scored 56.46% testing accuracy in evaluation. 

**More results and diagrams comprising the accuracy and realtion with respect to SNR can be found in the Evalution notebook**

# References and papers used: 
1- [T. O’shea, N. West “Radio Machine Learning Dataset Generation with
GNU Radio”](https://pubs.gnuradio.org/index.php/grcon/article/download/11/10/)

2-[T. O’Shea, J. Corgan, and T. Clancy “Convolutional Radio
Modulation Recognition Networks](https://arxiv.org/pdf/1602.04105.pdf)

3-[N. West, T. O’shea “Deep Architectures for Modulation Recognition”](https://arxiv.org/pdf/1703.09197.pdf)

5-[K. Karra, S. Kuzdeba, J. Peterson “Modulation recognition using
hierarchical deep neural networks”](http://ieeexplore.ieee.org/document/7920746/?anchor=authors)

