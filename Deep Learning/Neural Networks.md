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
In order to model sequences, we need to be able to handle variable-length (non-fixed length) sequences. They also need to track long-term dependencies, where a variable at a smaller time step may influence an outcome near the end of the time steps. Order needs to be maintained, and parameters need to be shared across the sequence. 

We can do all this with [[Recurrent Neural Networks]]. 

### Predict the Next Word
This is an example for a sequencing problem. Imagine we have this sentence:
"This morning I took my cat for a \_\_\_\_."
The next word is *walk*, but the model doesn't know that. How do we get it to guess?

First, we need to represent words as numbers. This is so the neural network can understand and predict words. This is also known as **encoding**. 
One idea for doing this is by creating a **vocabulary** of all words that the model will understand, index all words into a vector (so *a* might be 0, *cat* might 1, etc.). Finally, we can embed the indices of those words into a one-hot encoded vector. For example, *a* might be $[1, 0, 0, ..., 0]$, *cat* might be $[0, 1, 0, ..., 0]$, etc. 
Alternately, we can use a neural network to map words to an embedded state. 