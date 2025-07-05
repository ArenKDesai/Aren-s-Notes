Data Parallelism trains a model in parallel, but Model Parallelism trains a model over multiple GPUs. There are five strategies in the TensorFlow API:
1. MirroredStrategy: Synchronized training over multiple GPUs w/ one machine
2. CentralStorageStrategy: same as abocv