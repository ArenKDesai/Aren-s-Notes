#MIT #DeepLearning #ML

Extended from [[Neural Networks]]. 
We can keep the hidden layer the same, but isolate each input $x_t$ to run sequentially instead of parallel. Next, while we still compute the outputs $\hat{y}$ of the neurons (perceptrons), we also send the output of the hidden layer $h$ to the next sequential neuron. This idea is **recurrence** in neural networks, modelled by the function:
$\hat{y}_t=f(x_t,h_{t-1})$
where $\hat{y}_t$ is the output, $x_t$ is the input, and $h_{t-1}$ is the past memory. The function above is called the **recurrence relation**. The network built from recurrences is a **recurrent neural network** (RNN). 
![[rnn.png]]
The recurrence relations are defined by the cell states:
$h_t=f_W(x_t,h_{t-1})$
where $h_t$ is the cell state, $f_W$ is the function with weights $W$, $x_t$ is the input, and $h_{t-1}$ is the old state. 
Each of these $h$ states has its own loss value $L_t$, corresponding with a total loss for the RNN $L$. 

Unfortunately, RNNs are slow and, since they rely on iterative time-steps, cannot be parallelized. Long-term memory is a struggle, too. 

### Backpropagation through Time
The backpropagation takes the derivative of the loss with respect to each parameter and shifts those parameters in order to minimize loss. Both the forward and backward pass are included for Recurrent Neural Networks (RNNs), but there's another step of backpropagating through time steps as well. 

### Long-Short Term Memory (LSTM) Networks
There's a problem, though. This is **exploding and vanishing gradients**, which occur when large models with long-term dependencies fall into extremely large or small numbers in the gradient that lose value. This can be fixed with LSTMs that rely on a gated cell to track information through time steps. 

## Attention
A better way to make RNNs is to utilize **attention**, which consists of:
1. Identifying which parts of a dataset (image, for example) to attend to. This is similar to a search problem
2. Extracting those features with high attention
We can compute the search as such:
3. Compute the attention mask. How similar is each **key** to the desired **query**?
Next, we want to identify and attend to the most important features in the input. To do this:
4. Encode **position** information (such as location of words in a phrase)
5. Extract **query**, **key**, and the **value** for search. 
6. Compute **attention weighting**. The weight indicates where we should attend to. Here's a sample equation:
$\text{softmax}(\frac{Q\cdot K^T}{\text{scaling}})$
7. Extract features with high attention. 
![[Screenshot 2025-03-30 160056.png]]
All of these operations form the **self-attention head** that can be input into a larger network, where each head attends to different parts of an input. 
![[Screenshot 2025-03-30 160347.png]]