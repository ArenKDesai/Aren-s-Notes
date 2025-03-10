#MIT #DeepLearning #ML 

Neural networks (NNs) are made up of layers of perceptrons which map an input $x$ to an output $y$ with a linear function and a non-linear activation after. The number of layers between the input and output, called **hidden layers**, is variable. 
NNs use a **loss function** to determine how well the NN is doing at prediction. This is typically **Mean Squared Error** (MSE), but can be many other options. 
NNs use a **stochastic gradient descent** (SGD) algorithm to optimize the perceptron functions. This uses calculus to determine the direction to move the parameters that would minimize the loss function. The SGD algorithm moves backwards through the perceptrons in a process known as **backwards propagation**. 
NNs also rely on a **learning rate**, which dictates the rate at which the perceptron functions update. This is variable. 
NNs are also subject to **overfitting**, which is where the networks fit themselves too well to the data. This is typically fixed with **regularization**, which forces the NN to drop perceptrons at random to avoid relying on one too much. 

## Sequence Modelling
Examples of basic modelling tasks include:
- Binary Classification (1-1): Modelling inputs to a binary output. For example, asking a neural network to question if an event will occur or not occur. 
- Sentiment Classification ($N$-1): Modelling multiple inputs to a classification output. For example, reading tweets and classifying the sentiment as positive or negative. 
- Image Captioning (1-$N$): Modelling one input to a few outputs. For example, writing the description for an image. 
- Machine Translation ($N$-$M$): Mapping many inputs to many outputs. For example, translating one language to another. 
However, we can't take advantage of sequential time steps this way.  

We can keep the hidden layer the same, but isolate each input $x_t$ to run sequentially instead of parallel. Next, while we still compute the outputs $\hat{y}$ of the neurons (perceptrons), we also send the output of the hidden layer $h$ to the next sequential neuron. This idea is **recurrence** in neural networks. 