#DeepLearning #ML #MachineLearning #Statistics 

Whitepaper proposing Temporal Fusion Transformers (2019): [Temporal Fusion Transformers for Interpretable Multi-horizon Time Series Forecasting](https://arxiv.org/abs/1912.09363)

## Purpose
For forecasting or prediction tasks that are highly temporal and multi-horizon (non-singular prediction outcome), we might want a powerful model that's also highly explainable. The temporal fusion transformer (TFT) is an explainable architecture with those qualities. It allows for predictions multiple time-steps into the future. 
Multi-horizon forecasting models usually have temporal information that's very difficult to organize, such as information about the future, static metadata, and historical time series data. We want to maintain as much integrity of the data as possible while modelling this information. 

The temporal fusion transformer is an **attention-based DNN architecture for multi-horizon forecasting with interpretability** without sacrificing performance. It does so with static covariate encoders, gating mechanisms and sample-dependent variable selection, a sequence-to-sequence layer, and a temporal self-attention decoder. 

### Related Work

As of the writing of the paper, deep learning methods could be categorized into iterative autoregressions or direct sequence-to-sequence models. The iterative models typically assume that the values of all variables excluding the target are known at forecast time (which typically isn't true), and deep learning methods typically aren't explainable. Direct methods aren't very good at multi-horizon forecasts with multiple time steps. 

Previous time-series work doesn't consider static covariates, but the TFT architecture uses a separate encoder-decoder attention for static features at each time step, which determines the contribution of time-varying inputs. 

## Multi-Horizon Forecasting
Let there be $I$ unique MISO nodes in our time-series dataset. Each MISO node is associated with a 