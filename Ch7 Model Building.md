Data Parallelism trains a model in parallel, but Model Parallelism trains a model over multiple GPUs. There are five strategies in the TensorFlow API:
1. MirroredStrategy: Synchronized training over multiple GPUs w/ one machine
2. CentralStorageStrategy: same as above but with no mirroring
3. MultiWorkerMirroredStrategy: training is distributed across abstracted workers which could have multiple GPUs or machines
4. TPUStrategy: training over multiple TPU cores
5. ParameterServerStrategy: Some machines are designated as workers and some as parameter servers