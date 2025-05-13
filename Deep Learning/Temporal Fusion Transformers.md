#DeepLearning #ML #MachineLearning #Statistics 

Whitepaper proposing Temporal Fusion Transformers: [Temporal Fusion Transformers for Interpretable Multi-horizon Time Series Forecasting](https://arxiv.org/abs/1912.09363)

## Purpose
For forecasting or prediction tasks that are highly temporal and multi-horizon (non-singular prediction outcome), we might want a powerful model that's also highly explainable. The temporal fusion transformer (TFT) is an explainable architecture with those qualities. It allows for predictions multiple time-steps into the future. 
Multi-horizon forecasting models usually have temporal information that's very difficult to organize, such as information about the future, static metadata, and historical time series data. We want to maintain as much integrity of the data as possible while modelling this information. 

The temporal fusion transformer is an attention-based DNN architecture for multi-horizon forecasting with interpretability without sacrificing performance. It does so with static covariate encoders, gating mechanisms and sample-dependent variable selection, a sequence-to-sequence layer, and a temporal self-attention decoder. 