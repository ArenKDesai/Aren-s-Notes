## Sequences
In order to model sequences, we need to be able to handle variable-length (non-fixed length) sequences. They also need to track long-term dependencies, where a variable at a smaller time step may influence an outcome near the end of the time steps. Order needs to be maintained, and parameters need to be shared across the sequence. 

### Predict the Next Word
This is an example for a sequencing problem. Imagine we have this sentence:
"This morning I took my cat for a \_\_\_\_."
The next word is *walk*, but the model doesn't know that. How do we get it to guess?

First, we need to represent words as numbers. This is so the neural network can understand and predict words. This is also known as **encoding**. 
One idea for doing this is by creating a **vocabulary** of all words that the model will understand, index all words into a vector (so *a* might be 0, *cat* might 1, etc.). Finally, we can embed the indices of those words into a one-hot encoded vector. For example, *a* might be $[1, 0, 0, ..., 0]$, *cat* might be $[0, 1, 0, ..., 0]$, etc. 
Alternately, we can use a neural network to map words to an embedded state. 

### Backpropagation through Time
The backpropagation takes the derivative of the loss with respect to each parameter and shifts those parameters in order to minimize loss. Both the forward and backward pass are included for Recurrent Neural Networks (RNNs), but there's another step of backpropagating through time steps as well. 

## Long-Short Term Memory (LSTM) Networks
There's a problem, though. This is **exploding and vanishing gradients**, which occur when large models with long-term dependencies fall into extremely large or small numbers in the gradient that lose value. This can be fixed with LSTMs that rely on a gated cell to track information through time steps. 

### RNN problems
RNNs are slow and, since they rely on iterative time-steps, cannot be parallelized. Long-term memory is a struggle, too. 

## Attention
A better way to make RNNs is to utilize **attention**, whi