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

### Backpropagation through Time
The backpropagation takes the derivative of the loss with respect to each parameter and shifts those parameters in order to minimize loss. Both the forward and backward pass are included for Recurrent Neural Networks (RNNs), but there's another step of backpropagating through time steps as well. 

### Long-Short Term Memory (LSTM) Networks
There's a problem, though. This is **exploding and vanishing gradients**, which occur when large models with long-term dependencies fall into extremely large or small numbers in the gradient that lose value. This can be fixed with LSTMs that rely on a gated cell to track information through time steps. 