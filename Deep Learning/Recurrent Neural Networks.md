
Extended from [[Neural Networks]]. 
We can keep the hidden layer the same, but isolate each input $x_t$ to run sequentially instead of parallel. Next, while we still compute the outputs $\hat{y}$ of the neurons (perceptrons), we also send the output of the hidden layer $h$ to the next sequential neuron. This idea is **recurrence** in neural networks, modelled by the function:
$\hat{y}_t=f(x_t,h_{t-1})$
where $\hat{y}_t$ is the output, $x_t$ is the input, and $h_{t-1}$ is the past memory. The function above is called the **recurrence relation**. The network built from recurrences is a **recurrent neural network** (RNN). 
![[rnn.png]]
The recurrence relations are defined by the cell states:
$h_t=f_W(x_t,h_{t-1})$
where $h_t$ is the cell state, $f_W$ is the function with weights $W$, $x_t$ is the input, and $h_{t-1}$ is the old state. 
Each of these $h$ states has its own loss value $L_t$, corresponding with a total loss for the RNN $L$. 